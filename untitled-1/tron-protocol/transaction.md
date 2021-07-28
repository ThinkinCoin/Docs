# Transaction

## Generating Signed Transaction <a id="generating-signed-transaction"></a>

You can use Tronweb to complete the tasks of this section, for more details, please refer to: [Tronweb Github](https://github.com/tronprotocol/tronweb) [Tronweb API 文档](https://developers.tron.network/reference)​

Alternatively, you can use [API Signature and Broadcast Flow](https://developers.tron.network/docs/api-sign-flow) to generate a signed transaction.

The above document shows the complete workflow of using APIs, Here is mainly Tronweb, using freezeBalance as an example.

### Creating a Transaction <a id="creating-a-transaction"></a>

Create an unsigned transaction for freezing balance. [Tronweb freezeBalance](https://developers.tron.network/reference#freezebalance)​

### Signing the Transaction <a id="signing-the-transaction"></a>

Sign the transaction with your private key. [Tronweb sign](https://developers.tron.network/reference#sign)​

> #### ❗️ <a id="undefined"></a>
>
> Never use this in any web / user-facing applications, as it will expose your private key. For security reasons, please use a local full node.

### Broadcast the Transaction <a id="broadcast-the-transaction"></a>

Broadcast the signed transaction. [Tronweb Broadcast transaction](https://developers.tron.network/reference#sendrawtransaction)​

> #### 📘 <a id="undefined-1"></a>
>
> The broadcasting function in Tronweb is `sendrawtransaction` without a 'broadcast' keyword, refer to the [source code](https://github.com/tronprotocol/tronweb/blob/master/test/helpers/broadcaster.js) for details.

### Full Code Example <a id="full-code-example"></a>

JavaScript

```text
const CryptoUtils = require("@tronscan/client/src/utils/crypto");const TransactionUtils = require("@tronscan/client/src/utils/transactionBuilder");​function transferContractTx() {    const privateKey = "b815adfd6ef133d5a878869cb3a2b31f32d4c1481132a71300c3e125be0ab1a1";    const token = "TRX";    const fromAddress = CryptoUtils.pkToAddress(privateKey);    const toAddress = "TQ6pM81JDC2GhrUoNYtZGvPc7SvyqcemEu";    const amount = 1;​    let transaction = TransactionUtils.buildTransferTransaction(token, fromAddress, toAddress, amount);​    let signedTransaction = CryptoUtils.signTransaction(privateKey, transaction);}
```

## Transaction Confirmation <a id="transaction-confirmation"></a>

The mechanism of TRON's block validation is that a block is validated after this block is produced and 19 different SRs produce subsequent blocks based on this block.

When a block is confirmed, transactions inside are all confirmed. TRON provides the /walletsolidty/ interface to make it easier for users to search for confirmed transactions; the following describes how to confirm different types of transactions.

## Multi-type transactions <a id="multi-type-transactions"></a>

There are many types of transactions in TRON network: [protobuf](https://github.com/tronprotocol/java-tron/blob/develop/protocol/src/main/protos/core/Tron.proto#L307) [TRONWEB.TRANSACTIONBUILDER](https://cn.developers.tron.network/reference#applyforsr) Please read these contents for more details.

