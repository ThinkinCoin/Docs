# Query TRC-10 balance

**HTTP API:**HTTP

```text
wallet/getaccount
Description: Query an account information

demo: curl -X POST  http://127.0.0.1:8090/wallet/getaccount -d 
'{
    "address": "41E552F6487585C2B58BC2C9BB4492BC1F17132CD0"
}'
Parameter address: Default hexString
Return: Account object
```

**Tronweb Example:**JavaScript

```text
const privateKey = "..."; 
var address = "TM2TmqauSEiRf16CyFgzHV2BVxBejY9iyR";  
//Query the information of an account, and check the balance by assetV2 in the return value.
const tradeobj = await tronWeb.trx.getAccount(
      address,
);
console.log('- Output:', tradeobj, '\n');
```

**Wallet-cli Example :**wallet-cli commamd

```text
#Usage : GetAccount Address
GetAccount TWbcHNCYzqAGbrQteKnseKJdxfzBHyTfuh
```

