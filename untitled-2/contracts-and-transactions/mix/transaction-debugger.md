# Transaction debugger

Mix supports both Solidity and assembly level contract code debugging. You can toggle between the two modes to retrieve the relevant information you need.

At any execution point the following information is available:

VM stack – See Yellow Paper for VM instruction description

Call stack – Grows when contract is calling into another contract. Double click a stack frame to view the machine state in that frame

Storage – Storage data associated with the contract

Memory – Machine memory allocated up to this execution point

Call data – Transaction or call parameters

## Accessing the debug mode[¶](transaction-debugger.md)​ <a id="accessing-the-debug-mode"></a>

When transaction details are expanded, you can switch to the debugger view by clicking on the “Debug Transaction” button

## Toggling between debug modes and stepping through transactions[¶](transaction-debugger.md)​ <a id="toggling-between-debug-modes-and-stepping-through-transactions"></a>

This opens the Solidity debugging mode. Switch between Solidity and EVM debugging mode using the Menu button \(Debug -&gt; Show VM code\)

* Step through a transaction in solidity debugging mode
* Step through a transaction in EVM debugging mode

