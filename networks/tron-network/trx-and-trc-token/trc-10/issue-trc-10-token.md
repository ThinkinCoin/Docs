# Issue TRC-10 token

**HTTP API:**HTTP

```text
wallet/createassetissue
Description: Issue a token
demo: curl -X POST  http://127.0.0.1:8090/wallet/createassetissue -d '{
"owner_address":"41e552f6487585c2b58bc2c9bb4492bc1f17132cd0",
"name":"0x6173736574497373756531353330383934333132313538",
"abbr": "0x6162627231353330383934333132313538",
"total_supply" :4321,
"trx_num":1,
"num":1,
"start_time" : 1530894315158,
"end_time":1533894312158,
"description":"007570646174654e616d6531353330363038383733343633",
"url":"007570646174654e616d6531353330363038383733343633",
"free_asset_net_limit":10000,
"public_free_asset_net_limit":10000,
"frozen_supply":{"frozen_amount":1, "frozen_days":2}
}'
Parameter owner_address: Owner address, default hexString  
Parameter name: Token name, default hexString    
Parameter abbr: Token name abbreviation, default hexString  
Parameter total_supply: Token total supply    
Parameter trx_num: Define the price by the ratio of trx_num/num,
Parameter num: Define the price by the ratio of trx_num/num   
Parameter start_time: ICO start time
Parameter end_time: ICO end time    
Parameter description: Token description, default hexString
Parameter url: Token official website url, default hexString   
Parameter free_asset_net_limit: Token free asset net limit   
Parameter public_free_asset_net_limit: Token public free asset net limit    
Parameter frozen_supply: Token frozen supply  
Parameter permission_id: Optional, for multi-signature use    
Return: Transaction object
Note: The unit of 'trx_num' is SUN
```

**Tronweb Example：**JavaScript

```text
const privateKey = "...";
var createAssetAddress = "TM2TmqauSEiRf16CyFgzHV2BVxBejY9iyR"; 
const trc_options = {
      name : "test",
      abbreviation : "tt",
      description : "fortest",
      url : "www.baidu.com",
      totalSupply : 10000000,
      trxRatio : 1,
      tokenRatio : 1,
      saleStart : 1581929489000,
      saleEnd : 1581938187000,
      freeBandwidth : 0,
      freeBandwidthLimit : 0,
      frozenAmount : 0,
      frozenDuration : 0,
      precision : 6
}
//Create an unsigned transaction that issue trc10 token，equivalent to createToken
const tradeobj = await tronWeb.transactionBuilder.createAsset(
      trc_options,
      createAssetAddress
).then(output => {
  console.log('- Output:', output, '\n');
  return output;
});
//sign 
const signedtxn = await tronWeb.trx.sign(
      tradeobj,
      privateKey
);
//broadcast 
const receipt = await tronWeb.trx.sendRawTransaction(
      signedtxn
).then(output => {
  console.log('- Output:', output, '\n');
  return output;
});
```

**Wallet-cli Example :**wallet-cli command

```text
#Usage : AssetIssue [OwnerAddress] AssetName AbbrName TotalSupply TrxNum AssetNum Precision StartDate EndDate Description Url FreeNetLimitPerAccount PublicFreeNetLimit FrozenAmount0 FrozenDays0 ... FrozenAmountN FrozenDaysN
AssetIssue TestToken TT 100000 1 1 6 "2020-02-19 22:25:00" "2020-03-20" "This is a TRC10 Token" "https://shasta.tronscan.org/" 0 0
```

Please follow the instructions below to complete this transaction:

1. Tip: "Please confirm and enter your permission id, if input y or Y means default 0, other non-numeric characters will cancel transaction.", Enter "y" or "Y" to confirm the transaction;
2. Tip: "lease choose your key for sign. ...... Please choose between 1 and 2", select the serial number of the sign account;
3. Tip: "Please input your password.", Enter your local password;
4. Tip: "AssetIssue TestToken successful !!", which indicates that successfully issued TRC10 tokens.

