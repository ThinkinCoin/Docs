# TRC-721 Contract Interaction

## 1 Query the Token Name

Call the function ‘name\(\)’ of TRC-721 to get the token name.Shell

```text
curl -X POST https://api.shasta.trongrid.io/wallet/triggersmartcontract -d '{
           "contract_address":"418c921721ababd66313981e1ad49b19c4e799f24d",
           "function_selector":"name()",
           "owner_address":"411fafb1e96dfe4f609e2259bfaf8c77b60c535b93"
 }'
```

Result:Shell

```text
Result:
{"result":{"result":true},"constant_result":["0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000f596f757220546f6b656e204e616d650000000000000000000000000000000000"],"transaction":{"ret":[{}],"visible":false,"txID":"418a8fe76cb888e06c68cbe6a7c52b3b6f9c009877e16a2a87183868c5cbb1b0","raw_data":{"contract":[{"parameter":{"value":{"data":"06fdde03","owner_address":"411fafb1e96dfe4f609e2259bfaf8c77b60c535b93","contract_address":"418c921721ababd66313981e1ad49b19c4e799f24d"},"type_url":"type.googleapis.com/protocol.TriggerSmartContract"},"type":"TriggerSmartContract"}],"ref_block_bytes":"2d6d","ref_block_hash":"08e5816e980173a0","expiration":1615822557000,"fee_limit":400000000,"timestamp":1615822500321},"raw_data_hex":"0a022d6d220808e5816e980173a040c89e9eb4832f5a6d081f12690a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412340a15411fafb1e96dfe4f609e2259bfaf8c77b60c535b931215418c921721ababd66313981e1ad49b19c4e799f24d220406fdde0370e1e39ab4832f90018088debe01"}}
```

The name of the token is included in constant\_result, returned with the format of hex string.

Since the return value is string type, string in the virtual machine is considered to be a variable-length type. Its data contains two parts: length and actual value. Therefore, the above return value needs to be parsed into three parts, which is split every 32 bytes.

0000000000000000000000000000000000000000000000000000000000000020 pointer

000000000000000000000000000000000000000000000000000000000000000F length

596F757220546F6b656e204e616d650000000000000000000000000000000000 real value

Parsed to semantics, the string data is read from the 32nd byte \(20 in hexadecimal represents 32 in decimal\), and the length is 15 bytes. The actual data is "596F757220546F6b656e204e616d65". convert it into a string form is "Your Token Name".

## 2 Query the Token Symbol

Shell

```text
curl -X POST  https://api.shasta.trongrid.io/wallet/triggersmartcontract -d '{
           "contract_address":"418c921721ababd66313981e1ad49b19c4e799f24d",
           "function_selector":"symbol()",
           "owner_address":"411fafb1e96dfe4f609e2259bfaf8c77b60c535b93"
  }'
```

The symbol of the token is included in constant\_result\(YTN\), returned with the format of hex string.

The parsing process is similar to the name\(\) method above, please refer to the detailed explanation of `name()`.

## 3 Query the Balance

Shell

```text
curl -X POST https://api.shasta.trongrid.io/wallet/triggersmartcontract  -d '{
    "contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"balanceOf(address)",
"parameter":"000000000000000000000041977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
 }'
```

**Parameters**:

Contract\_address: contract address in hex string

Owner\_address: the account address which triggers the contract function in hex string

Function\_selector: the function to be called

Parameters need to be passed to the contract methods. In this case, the address should be passed in. In this case, the address should be passed in. Since the address structure of TRON is the address prefix "41" + 20-byte address, 32 bytes are required when the address parameters are transmitted, so fill it with "0" in front.

## 4 NFT Transfer

Shell

```text
curl -X POST https://api.shasta.trongrid.io/wallet/triggersmartcontract  -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"fee_limit": 400000000,
"function_selector":"transferFrom(address,address,uint256)",
"parameter":"0000000000000000000000001fafb1e96dfe4f609e2259bfaf8c77b60c535b9300000000000000000000000021ae4e504e68a75521221163faae1acd01deb3160000000000000000000000000000000000000000000000000000000000000001",
"call_value":0,
"owner_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182"
 }'
```

The parameter is to encode the address and uint256 in transfer\(address,uint256\), please refer to the [parameter encoding and decoding document](https://developers.tron.network/docs/parameter-and-return-value-encoding-and-decoding) for details.

> #### 📘Note
>
> After calling this HTTP API, signing and broadcast APIs should also be called.

Reference of transaction confirmation: [How to Confirm a Transaction](https://developers.tron.network/docs/transaction-11)

## 5 Approve the Control of an NFT to Another Address

Shell

```text
curl -X POST https://api.shasta.trongrid.io/wallet/triggersmartcontract  -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"fee_limit": 400000000,
"function_selector":"approve(address,uint256)",
"parameter":"000000000000000000000000173ebb4f23dbdc69f31065d7f8d2dacab32e004f0000000000000000000000000000000000000000000000000000000000000001",
"call_value":0,
"owner_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182"
 }'
```

The parameter is to encode the address and uint256 in transfer\(address,uint256\), please refer to the parameter encoding and decoding document for details.

> #### 📘Note
>
> After calling this HTTP API, signing and broadcast APIs should also be called.

Reference of transaction confirmation: [How to Confirm a Transaction](https://developers.tron.network/docs/transaction-11)

## 6 Query All NFT information of a TRC-721 Contract of a Specific Address

* Call the function of balanceOf\(address \_owner\) to query the number of NFT holdings
* Call the function of tokenOfOwnerByIndex\(address \_owner, uint256 \_index\) to traverse all token\_ids
* Call the function of tokenURI\(uint256 \_tokenId\) to query the details of every NFT.

