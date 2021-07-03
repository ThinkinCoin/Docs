# Multi-Signature

## Introduction

Multiple signature functions allow for permission grading, and each permission can correspond to multiple private keys. This makes it possible to achieve multi-person joint control of accounts. This guide walks the user through TRON's multi-signature implementation and design.

[https://github.com/tronprotocol/TIPs/blob/master/tip-16.md](https://github.com/tronprotocol/TIPs/blob/master/tip-16.md)

## Design

The scheme includes the three privilege levels of owner, duration, and active privilege. Owner privilege has the authority to execute all contracts, duration privilege is used for super delegates, and active is a custom privilege \(can be combined with permission sets\).

### Structure Description

**1. Account Modification**

```text
message Account { 
   ... 
   Permission owner_permission = 31;
   Permission witness_permission = 32;
   repeated Permission active_permission = 33;
 }
```

Three permission attributes are added to the account structure, namely owner\_permission, witness\_permission, and active\_permission, where active\_permission is a list and can be specified up to 8.

**2. Contract Type Modification**

```text
message Transaction {
   message Contract {
     enum ContractType { 
       AccountCreateContract = 0; 
       ... 
       AccountPermissionUpdateContract = 46; 
       }
     }  
   }
 }
```

Added a transaction type AccountPermissionUpdateContract to update account permissions.

**3. AccountPermissionUpdateContract**

```text
message AccountPermissionUpdateContract {
   bytes owner_address = 1;
   Permission owner = 2;   
   Permission witness = 3; 
   repeated Permission actives = 4; 
 }
```

| Parameter | Description |
| :--- | :--- |
| owner\_address | The address of the account to be modified |
| owner | Modified owner permission |
| witness | Modified witness permission \(if it is a witness\) |
| actives | Modified actives permission |

This interface overrides the original account permissions, so if you only want to modify the owner permissions, the witness \(if it is a witness account\) and actives also need to be set.

**4. Permission**

```text
message Permission {
   enum PermissionType {
     Owner = 0;
     Witness = 1;
     Active = 2;
   }
   PermissionType type = 1; 
   int32 id = 2;     
   string permission_name = 3;
   int64 threshold = 4;
   int32 parent_id = 5; 
   bytes operations = 6;  
   repeated Key keys = 7;// 
 }
```

| Parameter | Description |
| :--- | :--- |
| PermissionType | Permission type, currently only supports three permissions. |
| id | The value is automatically set by the system, with Owner id=0 and Witness id=1. Active id is incremented from 2 onwards. When the contract is executed, the id is used to specify which permission to use. For example, if the owner permission is used, the id is set to 0. |
| permission\_name | Permission name, set by the user, limited to 32 bytes in length. |
| threshold | Threshold, the corresponding operation is allowed only when the sum of the weights of the participating signatures exceeds the domain value. Requires a maximum value less than the Long type. |
| parent\_id | Currently only 0 |
| operations | A total of 32 bytes \(256 bits\), each representing the authority of a contract, a 1 means the authority to own the contract. For operations=0x0100...00 \(hexadecimal\), ie 100...0 \(binary\), look at the Transaction.ContractType definition in proto. The id of the contract AccountCreateContract is 0, which means that the permission only has the implementation of AccountCreateContract. Permissions can be obtained using the "calculation example of operations in active permissions". |
| keys | The address and weight that jointly own the permission can be up to 5 keys. |

**5. Key**

```text
message Key {
   bytes address = 1;
   int64 weight = 2;
 }
```

| Parameter | Description |
| :--- | :--- |
| address | Address with this privilege |
| weight | This address has weight for this permission |

**6. Transaction Modification**

```text
message Transaction {
      ...
     int32 Permission_id = 5;
 }
```

Add a `Permission_id` field to the transaction, corresponding to `Permission.id`, which specifies which permission to use. The default is 0, which is the owner permission. It is not allowed to be 1, because the witness permission is only used for block creation and is not used to sign the transaction.

### Owner Permission

OwnerPermission is the highest privilege of the account, used to control the ownership of the user, adjust the privilege structure, and the Owner privilege can also execute all contracts.

The Owner privilege has the following characteristics:

1. The OwnerPermission address can be modified by OwnerPermission.
2. When OwnerPermission is empty, the account address is assumed to have owner permission by default.
3. When the account is newly created, the address of the account is automatically filled in the OwnerPermission, and the default domain value is 1, the only address in the keys is included and the weight is 1.
4. When the permissionId is not specified when the contract is executed, OwnerPermission is used by default.

### Witness Permission

The super representative can use this privilege to manage the block nodes. Non-witness accounts do not have this permission.

Example of usage scenario: A super representative deploys a block program on the cloud server. For account security, you can assign the block permission to another address. Since the address only has the outbound permission, there is no TRX rollout permission, and even if the private key on the server is compromised, TRX will not be lost.

Witness block production node configuration:

1. No special configuration is required when the witness permissions are not modified.
2. The block node modified to witness permission needs to be reconfigured. The configuration items are as follows:

```text
#config.conf

// Optional.The default is empty.
// It is used when the witness account has set the witnessPermission.
// When it is not empty, the localWitnessAccountAddress represents the address of the witness account,
// and the localwitness is configured with the private key of the witnessPermissionAddress in the witness account.
// When it is empty,the localwitness is configured with the private key of the witness account.
// Optional, default is empty.
// Used to set the durationPermission when the witness account is set.
// When the value is not empty, localWitnessAccountAddress represents the address of the witness account, and localwitness is the private key of the address in the durationPermission.
// When the value is empty, localwitness is configured as the private key of the witness account.

//localWitnessAccountAddress =

localwitness = [
  f4df789d3210ac881cb900464dd30409453044d2777060a0c391cbdf4c6a4f57
]
```

### Active Permissions

Active permission is used to provide a combination of permissions, such as providing a permission to perform only the creation of accounts and transfer functions.

Active permissions have the following features:

1. With the address of OwnerPermission can modify Active permissions
2. The address with the permission to execute AccountPermissionUpdateContract can also modify Active permissions
3. Support up to 8 combinations.
4. The id of the permission is automatically incremented from 2.
5. When the account is newly created, an Active permission is automatically created, and the address of the account is filled in. The default domain value is 1, and only the account address is included in the keys and the weight is 1.

### Cost

1. When using the account update permission, that is, the AccountPermissionUpdate contract, 100TRX is charged.
2. When using a multi-signature transaction, that is, a transaction that includes two or more signatures in the transaction, in addition to the transaction fee, 1TRX is charged.
3. The above fees can be revised by the proposal.

## API

### Modify Permissions

`AccountPermissionUpdateContract`, modify the permissions steps are as follows:

1. Use the interface `getaccount` to query the account and get the original permissions
2. Modify the permission
3. Create a contract, signature
4. Send a transaction

**http-demo**

```text
http://{{host}}:{{port}}/wallet/accountpermissionupdate


{
  "owner_address": "41ffa9466d5bf6bb6b7e4ab6ef2b1cb9f1f41f9700",
  "owner": {
    "type": 0,
    "permission_name": "owner",
    "threshold": 2,
    "keys": [{
        "address": "41F08012B4881C320EB40B80F1228731898824E09D",
        "weight": 1
      },
      {
        "address": "41DF309FEF25B311E7895562BD9E11AAB2A58816D2",
        "weight": 1
      },
      {
        "address": "41BB7322198D273E39B940A5A4C955CB7199A0CDEE",
        "weight": 1
      }
    ]
  },
  "actives": [{
    "type": 2,
    "permission_name": "active0",
    "threshold": 3,
    "operations": "7fff1fc0037e0000000000000000000000000000000000000000000000000000",
    "keys": [{
        "address": "41F08012B4881C320EB40B80F1228731898824E09D",
        "weight": 1
      },
      {
        "address": "41DF309FEF25B311E7895562BD9E11AAB2A58816D2",
        "weight": 1
      },
      {
        "address": "41BB7322198D273E39B940A5A4C955CB7199A0CDEE",
        "weight": 1
      }
    ]
  }]
}

For the definition and limitations of the parameter fields, please see Structure Description.
```

**Example of calculation of operations in active authority**

```text
public static void main(String[] args) {

  // Specify the contract id to be supported (see the Transaction.ContractType definition in proto), which contains all contracts except AccountPermissionUpdateContract(id=46)
  Integer[] contractId = {0, 1, 2, 3, 4, 5, 6, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 30, 31,
      32, 33, 41, 42, 43, 44, 45};
  List<Integer> list = new ArrayList<>(Arrays.asList(contractId)); 
  byte[] operations = new byte[32];
  list.forEach(e -> {
    operations[e / 8] |= (1 << e % 8);
  });
  
  //7fff1fc0037e0000000000000000000000000000000000000000000000000000
  System.out.println(ByteArray.toHexString(operations));
}
```

### Contract Execution

1. Create a transaction, the same as the construction process of a non-multiple signature transaction 2, specify the Permission\_id, the default is 0, indicating the owner-permission
2. The user A signs the post-signature transaction to B through other means.
3. User B signs, and the signed transaction is sent to C by other means. ... n. The last user who completed the signature broadcasts the transaction to the node. N+1, verify that the sum of the weights of the multi-signature is greater than the domain value, accept the transaction, otherwise reject the transaction

Code example:

[https://github.com/tronprotocol/wallet-cli/blob/develop/src/main/java/org/tron/demo/MultiSignDemo.java](https://github.com/tronprotocol/wallet-cli/blob/develop/src/main/java/org/tron/demo/MultiSignDemo.java)

### Other New Interfaces

For detailed interface description, please see Tron-http.md and wave field wallet RPC-API.md

1. Increase Signature

```text
curl -X POST  http://127.0.0.1:8090/wallet/addtransactionsign -d '{"transaction": "TransferContract", "privateKey": "permissionkey1"}'
 
rpc AddSign (TransactionSign) returns (TransactionExtention) {}
```

1. Query Signed Address

```text
curl -X POST  http://127.0.0.1:8090/wallet/getapprovedlist -d '{"transaction"}'
 
rpc GetTransactionApprovedList(Transaction) returns (TransactionApprovedList) { }
```

1. Query Transaction Signature Weight

```text
curl -X POST  http://127.0.0.1:8090/wallet/getsignweight -d '{"transaction"}'
 
rpc GetTransactionSignWeight (Transaction) returns (TransactionSignWeight) {}
```

The owner-permission and an active-permission are automatically generated during account creation. The owner-permission contains one key, with the permissions and thresholds both set as 1. The active-permission also contains a key with permissions and thresholds set at 1.

The operations are "7fff1fc0037e0000000000000000000000000000000000000000000000000000", which means all operations except AccountPermissionUpdateContract are supported.

