# TRX Transfer

**HTTP Api:**HTTP

```text
wallet/createtransaction
Description: Create a transfer transaction, if to address is not existed, then create the account on the blockchain

demo: curl -X POST  http://127.0.0.1:8090/wallet/createtransaction -d 
'{
    "to_address": "41e9d79cc47518930bc322d9bf7cddd260a0260a8d",
    "owner_address": "41D1E7A6BC354106CB410E65FF8B181C600FF14292",
    "amount": 1000
}'
Parameter to_address: To address, default hexString
Parameter owner_address: Owner address, default hexString
Parameter amount: Transfer amount
Parameter permission_id: Optional, for multi-signature use
Return: Transaction object
```

**Tronweb Example：**JavaScript

```text
const privateKey = "..."; 
var fromAddress = "TM2TmqauSEiRf16CyFgzHV2BVxBejY9iyR"; //address _from
var toAddress = "TVDGpn4hCSzJ5nkHPLetk8KQBtwaTppnkr"; //address _to
var amount = 10000000; //amount
//Creates an unsigned TRX transfer transaction
tradeobj = await tronWeb.transactionBuilder.sendTrx(
      toAddress,
      amount,
      fromAddress
);
const signedtxn = await tronWeb.trx.sign(
      tradeobj,
      privateKey
);
const receipt = await tronWeb.trx.sendRawTransaction(
      signedtxn
);
console.log('- Output:', receipt, '\n');
```

**Wallet-cli Example ：**wallet-cli command

```text
#Usage : SendCoin [OwnerAddress] ToAddress Amount
SendCoin TWbcHNCYzqAGbrQteKnseKJdxfzBHyTfuh 100
```

Please follow the instructions below to complete this transaction:

1. Tip: "Please confirm and enter your permission id, if input y or Y means default 0, other non-numeric characters will cancel transaction.", Enter "y" or "Y" to confirm the transaction;
2. Tip: "lease choose your key for sign. ...... Please choose between 1 and 2", select the serial number of the sign account;
3. Tip: "Please input your password.", Enter your local password;
4. Tip: "Send 100 Sun to TWbcHNCYzqAGbrQteKnseKJdxfzBHyTfuh successful !!", which indicates that the TRX transfer was successful.

