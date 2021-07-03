# VM Exception Handling

There are four types of exceptions that may be incurred during contract execution:

1. Asset-style Exception
2. Require-style Exception
3. Validation-style Exception
4. VMillegal-style Exception

The following generates an assert-style exception that throws an invalid opcode error, consuming all Energy \(including consumed and unconsumed Energy so far\):

1. If the array index you are accessing is too large or negative \(for example x\[i\] where i &gt;= x.length or i &lt; 0\).
2. If you access a fixed length of bytesN the index is too large or negative.
3. If you use zero as a divisor for division or modulo operations \(for example 5 / 0 or 23 % 0 \).
4. If you shift the negative digit.
5. If you convert a too large or negative value to an enumerated type.
6. If you call an uninitialized internal function type variable.
7. If you call the argument of the assert \(expression\), and the final result is false.
8. Timeout during contract execution.
9. If a JVMStackOverFlowException occurs.
10. If an OutofMem exception occurs, that is, memory exceeded 3M.
11. During contract operation, an overflow occurs, such as addition.

The following conditions generate a require-style exception, which throws a revert error, and only consume the already consumed energy, excluding the unconsumed energy.

1. Call `throw`
2. If you call the `require` parameter \(expression\) the final result is false.
3. If you call a function via a message, but the function does not end correctly \(for example, the function runs out of Energy, or throws an exception itself\). If Energy is not specified when the function is called, all Energy will be passed in and consumed. Only the Energy value is set to see the difference. This function does not include the low-level operations `call`, `send`, `delegatecall`, or `callcode`. Low-level operations do not throw an exception, but return `false` to indicate failure.
4. If you create a contract with the new keyword, but the contract is not created correctly \(because you can't specify Energy during contract creation, all Energy is passed in and consumed\).
5. If your contract receives TRX via a public function without a payable modifier \(including constructors, fallback functions, and generic public functions\).
6. `transfer()` fails
7. Call `revert()`
8. Reach the maximum function stack depth 64.

> ## 📘Note
>
> Both the assert-style and require-style cases cause the TVM to roll back. The reason for the fallback is that it cannot continue to be performed safely because the expected effect is not achieved. Since we want to preserve the atomicity of the transaction, the safest thing to do is roll back all changes. However, a deduction will be made.

The following conditions will result in a validation-style exception. The transaction will not be chained and will not consume any Energy.

1. The current version does not support Virtual Machines.
2. When creating a contract, the contract name exceeds 32 bytes.
3. When creating a contract, the proportion of caller resources consumed is not between \[0, 100\]
4. When the contract is created, a hash conflict occurs in the newly generated contract address, that is, the contract address has been generated.
5. Call value is not 0 if there is an insufficient balance.
6. Fee Limit is not within the legal range.
7. Send a constant request to a node that does not support constant.
8. The triggered contract does not exist in the database.

A VMillegal-style exception occurs in the following cases. This type of exception transaction will not be chained, but the node that sent the transaction will be penalized at the network layer for a period of time.

1. `OwnerAddress` and `OriginAddress` are not equal when creating a contract.
2. Broadcast a constant request.
3. The entry is a go\(\) exception that will be caught and processed in go\(\) and will not be passed outside of go\(\).

```text
public void go() {

    try {
      vm.play(program);

      result = program.getResult();

      // If there is Exception or Revert
      // Important：
      // Exception is thrown in the program settings. 
      // Revert is a Virtual Machine compiler written into bytecode in advance, arriving by jump. 
      if (result.getException() != null || result.isRevert()) {

        if (result.getException() != null) {
          // If Exception，will consume all Energy
          program.spendAllEnergy();
          // Set runtimeError to indicate the field of the error content
          runtimeError = result.getException().getMessage();
          // Throw an exception
          throw result.getException();
        } else {
          // If it is Revert and there is no Exception, just set the runtimeError field to indicate the error content. 
          runtimeError = "REVERT opcode executed";
        }

        // As long as Exception or Revert occurs, it will not commit. All state changes in the virtual machine execution process will not fall. 

      } else {
        // Without Exception and Revert, commit, all state changes during virtual machine execution will fall. 
        deposit.commit();
      }
    }
    catch (JVMStackOverFlowException e) {
        // TVM or JVM, JVMStackOverFlowException, flags exception. 
        // The JVMStackOverFLowException will only be caught in go(), which uses JVMStackOverFlowException that occurs in the contract called by call. Or the JVMStackOverFlowException that is called repeatedly. It won't catch up in play(), and will only be caught here. 
        result.setException(e);
        runtimeError = result.getException().getMessage();
    }
    // Catch all the content that can be thrown
    catch (Throwable e) {
      // Mark if the exception is unknown. 
      if (Objects.isNull(result.getException())) {
        result.setException(new RuntimeException("Unknown Throwable"));
      }
      // Ensures the runtimeError has a value
      if (StringUtils.isEmpty(runtimeError)) {
        runtimeError = result.getException().getMessage();
      }

    }
  }
  // After the go() function, result.getException() will not be used, and runtimeError will be filled in the transactionInfo.
```

1. The play\(\) function is where the virtual machine actually executes. There are three places that call play\(\), go\(\) \(described above\), callToAddress\(\) \(the CALL instruction is called, which is called in the contract\), and createContract\(\) \(CREATE directive, which is when the contract is created in the contract\). The latter two will not handle catching exceptions, and the exceptions thrown out of play will continue to be thrown out in the latter two.

```text
// Play will catch all RuntimeException, and throw a JVMStackOverFlowException (including StackOverflowError)
  public void play(Program program) {
    try {
      // An op virtual execution virtual machine
      while (!program.isStopped()) {
        // Step will first catch the RuntimeException, deduct the Energy, and then throw. 
        // At this time, it will stop the step and catch the RuntimeException first, then deduct the Energy ring. 
        this.step(program);
      }
    }
    catch (JVMStackOverFlowException e) {
      // Throw a JVMStackOverFlowException exception
      throw new JVMStackOverFlowException();
    } catch (RuntimeException e) {
      if (StringUtils.isEmpty(e.getMessage())) {
        // Put the RuntimeException thrown by the step() function into program.result.exception instead of throwing it out. 
        program.setRuntimeFailure(new RuntimeException("Unknown Exception"));
      } else {
        program.setRuntimeFailure(e);
      }
    } catch (StackOverflowError soe) {
      // Throw a JVMStackOverFLowException exception
      throw new JVMStackOverFlowException();
    } finally {
    }
  }
```

1. step\(\) function

```text
// Step first catches the RuntimeException, deducts the Energy, and then throws
// Note, the exceptions thrown here are all RuntimeException
public void step(Program program) {
  try {
    // If the op is illegal, an IllegalOperationException is thrown. In fact, the Invalid is written in advance in the bytecode, and the assert-style operation jumps to invalid. 
    OpCode op = OpCode.code(program.getCurrentOp());
    if (op == null) {
      throw Program.Exception.invalidOpCode(program.getCurrentOp());
    }
    switch (op) {
      // 1. Calculate the energy required for the op

      // 2. If deduction is not enough, throw an OutOfEnergyException
      program.spendEnergy(energyCost, op.name());
 
      // 3. Detect CPU time, timeout, then throw OutOfResourceException
      program.checkCPUTimeLimit(op.name());

      // 4. Actual execution of OP
      // The focus here is on the CREATE instruction and the CALL instruction. 
      // The steps inside are all similar: 
      // 4.1 When the depth is up，it will push 0 to stack，then return
      // 4.2 If there is value, the balance is insufficient, then push 0 to stack, and return
      // 4.3 If there is value, transfer failes, throwing an exception of type RuntimeException. 
      // 4.4 (Requires execution) to execute the virtual machine
      // 4.5 The result of executing the virtual machine, there is an exception. No exception will be thrown, only all Energy will be deducted and push 0 to stack. 
      // 4.6 The result of executing the virtual machine, if there is a revert, it will return Energy, and push 0 to stack. 
      // 4.7 Successful execution will return Energy and push 1 to stack.

      // Note：
      // Revert operation, and after exception, how to deal with, is determined by the virtual machine bytecode. Some will revert and some will be invalid. 
      // callToPrecompile fails, it will directly throw an exception of RuntimeException type
   }
 } catch (RuntimeException e) {
   // step will first catch the RuntimeException, deduct the Energy, and then throw
   program.spendAllEnergy();
   // Stop loop
   program.stop();
    // Throw an exception
    throw e;
  } finally {
  }
}
```

![](https://cdn.readme.io/img/book-icon.svg?1625079683213) Updated 10 months ago

* [Table of Contents](https://developers.tron.network/docs/vm-exception)
  * [Exception Types](https://developers.tron.network/docs/vm-exception#exception-types)
  * [Assert-style Exception](https://developers.tron.network/docs/vm-exception#assert-style-exception)
  * [Require-style Exception](https://developers.tron.network/docs/vm-exception#require-style-exception)
  * [Validation-style Exception](https://developers.tron.network/docs/vm-exception#validation-style-exception)
  * [VMillegal-style Exception](https://developers.tron.network/docs/vm-exception#vmillegal-style-exception)
  * [Exception Handling Process](https://developers.tron.network/docs/vm-exception#exception-handling-process)

