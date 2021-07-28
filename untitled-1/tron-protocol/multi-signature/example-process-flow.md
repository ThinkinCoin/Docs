# Example Process Flow

TronWeb allows developers to easily perform multi-signing with the `tronWeb.trx.multiSign` method. The is an example of the workflow.

## 1. Create transaction <a id="1-create-transaction"></a>

JavaScript

```text
const originalTransaction = await tronWeb.transactionBuilder.sendTrx('41e0d5217904dcb2d5453c2359b86df9673046c4ce', 100000, '4164eb61f763d3374a998989f06929c1bad87175ba');
```

## 2. Perform the Multi-Signing <a id="2-perform-the-multi-signing"></a>

JavaScript

```text
let signedTransaction = await tronWeb.trx.multiSign(originalTransaction, '47e5e1a590a44e7e6f4349a4e3ea6a4f9a791e3fccb115ffbddffdbf6d0588e6', 2);​signedTransaction = await tronWeb.trx.multiSign(signedTransaction, 'd5f244307d3ab6dc5739b83ec913b662a24f87e873190e9c1a2d9709f579540c', 2);​signedTransaction = await tronWeb.trx.multiSign(signedTransaction, '9944b7010db0d44a861bca112e40365a934727c5c17f8dfd3b9cc7b31e8aeaf1', 2);
```

Signature result:JSON

```text
{  "signature": [    "2c25a81333fd83edec33ebae16cb3dfb979cfc4ce035665953c2b61179b06cb9f0625c660947404c5a1e17331cc375579bed7295ebe6635eb30ab79e73c16e6a01",    "86cfad6c7bc086c04c27267ef4a3c5ae3ea394e05e8402713b0b7e624546b76e30518ebf897c7495b29bbb372ba94d65ba927bd48a4fa9c36e439c975b7f88f500",    "4d980f85de1a1bcc0c45fa118276a3a6319a6cf404ee68f5d460fb075bd41f6a8702e0448db2eb55cd74c4dd85d53909597eb05401a48aaa44bdb3a327e47d5001"  ],  "txID": "7034c0a26ffc1010c2cba113d9685cbe464793abe0a1d0d21c2e593df7990a84",  "raw_data": {    "contract": [      {        "parameter": {          "value": {            "amount": 100000,            "owner_address": "4164eb61f763d3374a998989f06929c1bad87175ba",            "to_address": "41e0d5217904dcb2d5453c2359b86df9673046c4ce"          },          "type_url": "type.googleapis.com/protocol.TransferContract"        },        "type": "TransferContract",        "Permission_id": 2      }    ],    "ref_block_bytes": "02d6",    "ref_block_hash": "cf96636fd7767b20",    "expiration": 1555454166000,    "timestamp": 1555454106555  },  "raw_data_hex": "0a0202d62208cf96636fd7767b2040f087acc2a22d5a69080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a154164eb61f763d3374a998989f06929c1bad87175ba121541e0d5217904dcb2d5453c2359b86df9673046c4ce18a08d06280270bbb7a8c2a22d"}
```

The method requires passing the original transaction, the private key for signing, and the permission ID. The permission ID should be generated when you update the account permission. You can overview your account permission and check the permission ID by calling the `getAccount` method.

Notes: If you use active permission, we will re-calculate the transaction ID, which differs from the original transaction after `tronWeb.transactionBuilder.sendTrx` or other methods.

## 3. Check Transaction's Sign Weight <a id="3-check-transactions-sign-weight"></a>

The function `tronweb.trx.getSignWeight`allows you to check how many addresses have signed the transaction and the current weight. This function can be run either during the multi-signing process or after its completion.JavaScript

```text
const signWeight = await tronWeb.trx.getSignWeight(signedTransaction, 2);
```

Result:JSON

```text
{  "result": {​  },  "approved_list": [    "4164eb61f763d3374a998989f06929c1bad87175ba",    "41e0d5217904dcb2d5453c2359b86df9673046c4ce",    "41e3222fff601087f76ee803c0e09596b21282f10d"  ],  "permission": {    "operations": "7fff1fc0037e0000000000000000000000000000000000000000000000000000",    "keys": [      {        "address": "4164eb61f763d3374a998989f06929c1bad87175ba",        "weight": 1      },      {        "address": "41e0d5217904dcb2d5453c2359b86df9673046c4ce",        "weight": 1      },      {        "address": "41e3222fff601087f76ee803c0e09596b21282f10d",        "weight": 1      }    ],    "threshold": 3,    "id": 2,    "type": "Active",    "permission_name": "active0"  },  "current_weight": 3,  "transaction": {    "result": {      "result": true    },    "txid": "7100eddcc788b0956e0224470111bffaa99b465781a2abe75cbd2a29c82ade42",    "transaction": {      "signature": [        "bfc89f7a49fa233cfb2484c5e1fdb3c687815c68f198fc81b0cccbc1ccbb09c611d0f3d90a32d7e8dc1d85fde43c10b7cb586edde1833f7974fda42e951b94ed00",        "8c167cd077d82f5b36e1d2bbc831711523dcc71494830cee6181b1435c44b22b751d6a72b425948db8aac3fb5f736bd2f9e689e18941002cafab1ff3caeb354d01",        "64921a4760fd2b2fb8f76bb7feab50d49d6298774f120164c050f4e154d624445e9a620b051116ec674f62640adb5ff2d6b0934ba9187db1197d65f368fd5ebc00"      ],      "txID": "7100eddcc788b0956e0224470111bffaa99b465781a2abe75cbd2a29c82ade42",      "raw_data": {        "contract": [          {            "parameter": {              "value": {                "amount": 100000,                "owner_address": "4164eb61f763d3374a998989f06929c1bad87175ba",                "to_address": "41e0d5217904dcb2d5453c2359b86df9673046c4ce"              },              "type_url": "type.googleapis.com/protocol.TransferContract"            },            "type": "TransferContract"          }        ],        "ref_block_bytes": "03a9",        "ref_block_hash": "f04705dfcc42a285",        "expiration": 1555454799000,        "timestamp": 1555454740761      },      "raw_data_hex": "0a0203a92208f04705dfcc42a2854098d9d2c2a22d5a69080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a154164eb61f763d3374a998989f06929c1bad87175ba121541e0d5217904dcb2d5453c2359b86df9673046c4ce18a08d062802709992cfc2a22d"    }  }}
```

## 4. Check Approved List <a id="4-check-approved-list"></a>

The function `tronWeb.trx.getApprovedList` allows you to check how many addresses have already signed \(approved\) the transaction.JavaScript

```text
const approvedList = await tronWeb.trx.getApprovedList(signedTransaction);
```

Result:JSON

```text
{  "result": {​  },  "approved_list": [    "4164eb61f763d3374a998989f06929c1bad87175ba",    "41e0d5217904dcb2d5453c2359b86df9673046c4ce",    "41e3222fff601087f76ee803c0e09596b21282f10d"  ],  "transaction": {    "result": {      "result": true    },    "txid": "479d294569f9d16bb9db643383eae40d4d6df0fa081b6918cf5d831f6fcac1bc",    "transaction": {      "signature": [        "fe5eaa06536e431143612d7b967059480ade185c70ad3c7529ed72c91b74b5c705cc231a857247e5cec31cb1aceb2d9016d2fb2bf57124ec5314b2b1688d060701",        "6951c7e651fdf79102d655acd6ed57e9c2ba8d4e9b7c1486b54c7d9912bf9e58bb5a4876593532f889858e819b41bb9ae60da7693a008fff7d335da34b9088e401",        "9960d832d5d71556124ea04e783e7e15d4437c27933b90d834670d58f590a3a255d3081d12b7ddccd8a84060ad1294b0c19f9ee63fa12fd5c602695ff32f8b6300"      ],      "txID": "479d294569f9d16bb9db643383eae40d4d6df0fa081b6918cf5d831f6fcac1bc",      "raw_data": {        "contract": [          {            "parameter": {              "value": {                "amount": 100000,                "owner_address": "4164eb61f763d3374a998989f06929c1bad87175ba",                "to_address": "41e0d5217904dcb2d5453c2359b86df9673046c4ce"              },              "type_url": "type.googleapis.com/protocol.TransferContract"            },            "type": "TransferContract"          }        ],        "ref_block_bytes": "03e5",        "ref_block_hash": "3dfe142fc7c242bf",        "expiration": 1555454979000,        "timestamp": 1555454919646      },      "raw_data_hex": "0a0203e522083dfe142fc7c242bf40b8d7ddc2a22d5a69080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a154164eb61f763d3374a998989f06929c1bad87175ba121541e0d5217904dcb2d5453c2359b86df9673046c4ce18a08d06280270de87dac2a22d"    }  }}
```

## 5. Broadcast Transaction <a id="5-broadcast-transaction"></a>

Once multi-signing completes, you can broadcast the signed transaction directly and check the transaction by using `getTransactionById` later.JavaScript

```text
const result = await = tronWeb.trx.broadcast(signedTransaction);
```

Result:JSON

```text
{  "result": true,  "transaction": {    "signature": [      "9ea568d070de64ce674d9db0d1c0dddbdf83435b4e60b27860fd7a017c071f9858062671ff938600b5cbd8b3475b2ab16df4c2076654f18a928e972ce3fe5e3600",      "202db297c8b31d51e1ad9406aaad030b602af865810a58d19910858bba3825ef0143b3013b33ad15aa6680b6b735efd1b8d5a913f42ed7d04792b9200f69097401",      "5c143c98ff4f9a7837eacd8ed26320b4a5544954241ca7985d73e6d099b1f8df0667d686e9e6ab5a2ae6be62e6795523b2cf423b3fc3a88523faf2408dac753001"    ],    "txID": "b25f3449384b0ea6b8c201596ed6998fb5581f4a68c5d467a268a4e60499ff1b",    "raw_data": {      "contract": [        {          "parameter": {            "value": {              "amount": 100000,              "owner_address": "4164eb61f763d3374a998989f06929c1bad87175ba",              "to_address": "41e0d5217904dcb2d5453c2359b86df9673046c4ce"            },            "type_url": "type.googleapis.com/protocol.TransferContract"          },          "type": "TransferContract",          "Permission_id": 2        }      ],      "ref_block_bytes": "0412",      "ref_block_hash": "614e7424dfcf96fb",      "expiration": 1555455114000,      "timestamp": 1555455056464    },    "raw_data_hex": "0a0204122208614e7424dfcf96fb4090f6e5c2a22d5a69080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a154164eb61f763d3374a998989f06929c1bad87175ba121541e0d5217904dcb2d5453c2359b86df9673046c4ce18a08d06280270d0b4e2c2a22d"  }}
```

