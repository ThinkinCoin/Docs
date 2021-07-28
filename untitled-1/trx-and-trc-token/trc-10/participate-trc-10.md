# Participate TRC-10

**HTTP API:**HTTP

```text
wallet/participateassetissueDescription: Participate a tokendemo: curl -X POST http://127.0.0.1:8090/wallet/participateassetissue -d '{"to_address": "41e552f6487585c2b58bc2c9bb4492bc1f17132cd0","owner_address":"41e472f387585c2b58bc2c9bb4492bc1f17342cd1", "amount":100, "asset_name":"3230313271756265696a696e67"}'Parameter to_address: The issuer address of the token, default hexString    Parameter owner_address: The participant address, default hexString Parameter amount: The number of trx participating in token issuanceParameter asset_name: Token id, default hexString         Parameter permission_id: Optional, for multi-signature use          Return: Transaction objectNote: The unit of 'amount' is the smallest unit of the token
```

**Tronweb Example：**JavaScript

```text
const privateKey = "..."; var issuerAddress = "TM2TmqauSEiRf16CyFgzHV2BVxBejY9iyR"; var tokenID= "1000088";var amount = 1000;var buyerAddress = "TVDGpn4hCSzJ5nkHPLetk8KQBtwaTppnkr";//Creates an unsigned ICO token purchase transaction.const tradeobj = await tronWeb.transactionBuilder.purchaseToken(      issuerAddress,      tokenID,      amount,      buyerAddress,    ).then(output => {  console.log('- Output:', output, '\n');  return output;});//sign const signedtxn = await tronWeb.trx.sign(      tradeobj,      privateKey);//broadcast const receipt = await tronWeb.trx.sendRawTransaction(      signedtxn).then(output => {  console.log('- Output:', output, '\n');  return output;});
```

**Wallet-cli Example :**wallet-cli command

```text
#Usage : ParticipateAssetIssue [OwnerAddress] ToAddress AssetID AmountParticipateAssetIssue TQmDzierQxEFJm1dT5YXnTXqVAfdN9HtXj 1000099 1000
```

Please follow the instructions below to complete this transaction:

1. Tip: "Please confirm and enter your permission id, if input y or Y means default 0, other non-numeric characters will cancel transaction.", Enter "y" or "Y" to confirm the transaction;
2. Tip: "lease choose your key for sign. ...... Please choose between 1 and 2", select the serial number of the sign account;
3. Tip: "Please input your password.", Enter your local password;
4. Tip: "ParticipateAssetIssue 1000099 1000 from TQmDzierQxEFJm1dT5YXnTXqVAfdN9HtXj successful !!", which indicates that Successfully participated in TRC10 tokens.

