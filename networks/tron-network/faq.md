# FAQ

**Answer**  
 Prevent the contract call transaction from consuming too much energy.

**Explanation**  
 The fee\_limit indicates the value of the total energy that a contract caller can tolerate at most for this transaction. The base unit is sun, and the maximum value can be set to 5e9. If the user does not set fee\_limit, the default value is 0. For example, if the fee\_limit is set to 1000 sun in the transaction, it means that the contract caller will endure the transaction and consume up to 100 energy \(the current unit price of energy is 140 sun\).

If the amount of energy consumed by the transaction execution exceeds the fee\_limit\*energy unit price, contract execution will be stopped and an OUT\_OF\_ENERGY error will be triggered.

In some contract functions, there will be complex loops. If the user calls it by mistake without knowing it, it may cause the user to consume too much energy, so the user can set this fee\_limit field as an upper limit.

There are some situations which cause all fee\_limit to be deducted:

* Illegal instruction encountered during contract execution
* Contract call timeout, trigger OUT\_OF\_TIME error
* if the array index you are accessing is too large or negative \(for example x\[i\] where i &gt;= x.length or i &lt; 0\).
* If you access a fixed length of bytesN the index is too large or negative.
* If you use zero as a divisor for division or modulo operations \(for example 5 / 0 or 23 % 0 \).
* If you shift the negative digit.
* If you convert a too large or negative value to an enum type.
* If you call an uninitialized internal function type variable.
* If you call the argument of the assert \(expression\), and the final result is false.
* If a JVMStackOverFlowException occurs.
* If an OutofMem exception occurs, that is, memory exceeded 3M.
* During contract operation, an overflow occurs, such as addition.

**Answer**  
 The contract function is too complex or the performance of the SR node fluctuates.

**Explanation**  
 At present, TRON has a global setting. The execution time of calling smart contract transactions cannot exceed 80ms. This 80ms parameter can be modified by SR voting. If the contract code is very complex and the execution time exceeds 80ms, it will trigger an OUT\_OF\_TIME error and deduct all fee\_limit fees.

If the same contract function sometimes triggers the OUT\_OF\_TIME error, sometimes it does not trigger the OUT\_OF\_TIME error, indicating that the complexity of the contract code is at a critical value. Because the machine performance of different SRs is different, it will cause intermittent triggering.

In addition, it should be noted that due to the fluctuation of SR machine performance, there will be a small probability that the contract function call with very low complexity will also trigger the OUT\_OF\_TIME error. It is recommended that users set the appropriate fee\_limit according to the contract complexity to prevent excessive losses caused by excessive setting of fee\_limit.

Base58 format: T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb  
 HexString format: 410000000000000000000000000000000000000000

**Answer**

1. First, according to txid, query the contractResult field in the result returned through the wallet/gettransactioninfobyid interface. If the field is not empty, you can see the abi code value of the message, convert the code value into a string, and find the reason for the error.  For example, txid:e5e013e81cb50a4c495a11c8130ad165a4e98d89b9e3fb5b79e6111bf23b31ed  Return contractResult data:  "contractResult": \[  "08c379a00000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000001e536166654d6174683a207375627472616374696f6e206f766572666c6f770000"  \]  Converting 1e536166654d6174683a207375627472616374696f6e206f766572666c6f77 into a string is: SafeMath: subtraction overflow, this transaction is because the transfer address overflowed during the subtraction operation during the transfer. The specific failure may be caused by insufficient balance. You need to check the address balance and transfer amount，Other errors can be checked according to the specific reason of the error.
2. If the contractResult is empty, it may be caused by the failure of the require assertion without message in the contract. For details, please refer to the [document](vm-exception-handling.md) and view the contract source code for analysis.

**Answer**

1. The bandwidth is calculated based on the number of bytes encoded by the transaction protobuf.
2. Energy is deducted based on the instructions executed by the contract. Different instructions are deducted differently. The more complex the contract, the more energy will be consumed. The energy consumed by the current contract can be estimated by testing on the testnet or viewing the previous historical calls of the contract through tronscan.  Resource model can refer to the [document](resource-model.md)

**Answer**  
 The transaction broadcast is successful but not on the chain because the transaction is not broadcast to the SR node because of the node's network or other unknown reasons. In this case, because the transaction has a validity period, it is best to add a delay judgment, and add it after the transaction validity period. If a little extra time is not on the chain, it can be judged that the transaction has exceeded the validity period, and the transaction can be initiated again, or the transaction can be rebroadcast within the validity period.

**Answer**

1. It is necessary to check whether the address of the calling contract has TRX and whether it is enough to pay for the burning energy or bandwidth cost, otherwise the address needs to obtain enough TRX.
2. If there is enough TRX, the feelimit set by the transaction is smaller, and the feelimit setting needs to be increased.

**Answer**  
 1.Improve machine configuration, recommend 16core 32GRAM 1T hard drive \(ssd\)

In the result of the following command, the maximum value of both cpu cores and siblings needs to be greater than or equal to 16.

$cat /proc/cpuinfo \| grep -e "cpu cores" -e "siblings" \| sort \| uniq  
 cpu cores : 8  
 siblings : 16  
 2.Increase the time tolerance of verification transactions  
 Increase the value of the maxTimeRatio configuration item in the node configuration file to 20.0 or higher.

vm = {  
 supportConstant = false  
 minTimeRatio = 0.0  
 maxTimeRatio = 20.0  
 saveInternalTx = false  
 }  
 3.Modify java-tron startup parameters to increase parallel garbage collection parameters：XX:+UseConcMarkSweepGC and -Xmx  
 like:  
 java -Xmx24g -XX:+UseConcMarkSweepGC -jar FullNode.jar -c .....  
 -XX:+UseConcMarkSweepGC should be placed before the -jar parameter, not at the end  
 -Xmx can be set to 80% of physical memory

**Answer**  
 If the number of unprocessed transactions of the node exceeds 2000, a server busy error will be returned. According to the machine situation, you can increase the PendingSize by modifying the node.maxTransactionPendingSize in the node configuration file. For example, set node.maxTransactionPendingSize = 5000.

**Answer**  
 Because TronGrid currently has an IP frequency limit for all TronGrid requests, the IP frequency is limited to 15QPS for TronGrid HTTP requests that use API Key. For TronGrid HTTP requests that without API Key, the current IP frequency is limited to 10QPS and will gradually decrease periodically. The current IP frequency limit for using the TronGrid GRPC service is 15QPS. If the frequency limit is exceeded, a 503 error will be returned. If a 503 error is reported, please reduce the frequency of the TronGrid request and it is recommended to add an API Key as soon as possible.

**Answer**  
 This issue is currently only seen when users downgrade the java-tron version from GreatVoyage-v4.2.2 \(Lucretius\) or other higher versions to GreatVoyage-v4.2.1 \(Origen\) \(or GreatVoyage-v4.2.0 \(Plato\)\). If users encounter this problem, they need to use a repair tool to repair the database. After the repair is complete, users can use GreatVoyage-v4.2.2.1 \(Epictetus\) or later versions to start the node normally. Please refer to the detailed operation steps from [DBReqair.jar User Guide](dbreqair.jar-user-guide.md)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Error Code</th>
      <th style="text-align:left">Cause</th>
      <th style="text-align:left">Solution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">SIGERROR</td>
      <td style="text-align:left">Signature error</td>
      <td style="text-align:left">
        <ol>
          <li>Check whether the private key used for the sign belongs to the address
            which sends the transaction.</li>
          <li>Check the format of the input private key.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">BANDWITH_ERROR</td>
      <td style="text-align:left">There is not enough bandwidth or TRX to burn to send a transaction.</td>
      <td
      style="text-align:left">Deposit TRX in the account, or use another account to delegate bandwidth
        to this account.</td>
    </tr>
    <tr>
      <td style="text-align:left">DUP_TRANSACTION_ERROR</td>
      <td style="text-align:left">Having broadcast a transaction with the same transaction hash with a former
        transaction.</td>
      <td style="text-align:left">
        <ol>
          <li>Rebuild a transaction.</li>
          <li>Change a node to broadcast.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">TAPOS_ERROR</td>
      <td style="text-align:left">The transaction and its reference block are not in the same chain.</td>
      <td
      style="text-align:left">
        <ol>
          <li>Change the field value of &apos;trx.reference.block&apos; to &quot;solid&quot;
            for transactions created by local nodes.</li>
          <li>Try to refer to the newest solidified block for transactions that are
            constructed locally.</li>
        </ol>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">TOO_BIG_TRANSACTION_ERROR</td>
      <td style="text-align:left">The transaction is too big, which may be caused by a too long memo.</td>
      <td
      style="text-align:left">Reduce the size of the transaction.</td>
    </tr>
    <tr>
      <td style="text-align:left">TRANSACTION_EXPIRATION_ERROR</td>
      <td style="text-align:left">The transaction is expired.
        <br />The default transaction expiration time is 60 seconds. If the time period
        between transaction creation and broadcast is over 60 seconds, the transaction
        will be regarded as expired.</td>
      <td style="text-align:left">Broadcast the transaction before its expiration time.
        <br />You may change the transaction validity period In your local node configuration.
        <br
        />Public node configurations can not be changed, the default expiration
        time is 60 seconds.</td>
    </tr>
    <tr>
      <td style="text-align:left">SERVER_BUSY</td>
      <td style="text-align:left">The whole network is busy.</td>
      <td style="text-align:left">Wait. Stagger the busy time of the network before.</td>
    </tr>
    <tr>
      <td style="text-align:left">NOT_ENOUGH_EFFECTIVE_CONNECTION</td>
      <td style="text-align:left">The reason is the node has not synchronized to the newest block.</td>
      <td
      style="text-align:left">Check the current block height on Tronscan, compare the height with the
        result of &apos;/wallet/getnowblock&apos; of the local node.</td>
    </tr>
    <tr>
      <td style="text-align:left">OTHER_ERROR</td>
      <td style="text-align:left">Unknown error.</td>
      <td style="text-align:left">The detailed error information can only be obtained through the node log.</td>
    </tr>
    <tr>
      <td style="text-align:left">CONTRACT_VALIDATE_ERROR</td>
      <td style="text-align:left">Transaction (system contract) verification failed</td>
      <td style="text-align:left">Any parameter error may cause this error, need to parse the error message
        to view the details. Common error messages are shown in the table below</td>
    </tr>
  </tbody>
</table>

| account does not exist | The account that initiated the transaction is not activated |
| :--- | :--- |
| Validate \*\*\* error, no OwnerAccount | The owner address is incorrect |
| No contract or not a valid smart contract | The contract address is incorrect |
| this node does not support constant | The vm.supportconstant of the node is not set to 1. This is common in self-built nodes. |

![](https://cdn.readme.io/img/book-icon.svg?1625079683213) Updated 3 days ago

* [Table of Contents](faq.md)
  * [1. Why do I need to submit the fee\_limit field when sending a transaction to call a smart contract？](faq.md#1-why-do-i-need-to-submit-the-fee_limit-field-when-sending-a-transaction-to-call-a-smart-contract%EF%BC%9F)
  * [2. Why would I trigger OUT\_OF\_TIME error when calling contract function?](faq.md#2-why-would-i-trigger-out_of_time-error-when-calling-contract-function)
  * [3. What is the destruction address of TRON?](faq.md#3-what-is-the-destruction-address-of-tron)
  * [4. How to troubleshoot when calling the contract and return the revert error?](faq.md#4-how-to-troubleshoot-when-calling-the-contract-and-return-the-revert-error)
  * [5. How to calculate the bandwidth and energy consumed when calling the contract?](faq.md#5-how-to-calculate-the-bandwidth-and-energy-consumed-when-calling-the-contract)
  * [6. After the transaction broadcast is successful, why can't it be queried on the chain?](faq.md#6-after-the-transaction-broadcast-is-successful-why-cant-it-be-queried-on-the-chain)
  * [7. How to solve "OUT\_OF\_ENERGY" error?](faq.md#7-how-to-solve-out_of_energy-error)
  * [8. How to solve the problem of slow node block synchronization or stop synchronization?](faq.md#8-how-to-solve-the-problem-of-slow-node-block-synchronization-or-stop-synchronization)
  * [9.How to solve SERVER\_BUSY error?](faq.md#9how-to-solve-server_busy-error)
  * [10.How to solve the error of TronGrid 503 Service Temporarily Unavailable?](faq.md#10how-to-solve-the-error-of-trongrid-503-service-temporarily-unavailable)
  * [11. How to solve no `Constant_result` in the transaction when user triggers the `pure` or `view` methods of the contract.](faq.md#11-how-to-solve-no-constant_result-in-the-transaction-when-user-triggers-the-pure-or-view-methods-of-the-contract)
  * [12. Broadcast Response Code](faq.md#12-broadcast-response-code)
  * [13. CONTRACT\_VALIDATE\_ERROR Common Error Messages Description](faq.md#13-contract_validate_error-common-error-messages-description)

