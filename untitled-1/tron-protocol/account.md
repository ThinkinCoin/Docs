# Account

## Introduction <a id="introduction"></a>

TRON uses an account model. The address is the unique identifier of an account, and a private key signature is required to operate an account. An account has many attributes, including TRX & token balances, bandwidth, energy, Etc. TRX's and tokens' transferring cost bandwidth, smart contract related operations cost energy. An account can apply to become a super representative candidate and accept votes from other accounts. The account is the basis of all the TRON's activities.

## Account creation <a id="account-creation"></a>

1. Generate the address and private key using a wallet or explorer. Use these 2 ways to activate the account: Transfer TRX/TRC-10 token to this address, the other way is transferring TRX/TRC-10 in a contract. This operation costs extra 25,000 energy.
2. Call the `CreateAccount` contract from an existing account.

Account creation costs only bandwidth. It burns TRX if bandwidth is insufficient.

Transferring TRC20 will not activate an account. However, the balance can be inquired from Tronscan by the address.

## Key-pair Generation <a id="key-pair-generation"></a>

Tron's signature algorithm is ECDSA, and the curve used is SECP256K1. A private key is a random number, and the corresponding public key is a point on the elliptic curve. Generating process:

1. Make a random number `d` as the private key.
2. Calculate `P = d * G` as the public key. \(`G` is the elliptic curve base point\)

## Address Format <a id="address-format"></a>

Use the public key `P` as the input, and use SHA3 get the result `H`. The length of the public key is 64 bytes \(SHA3 uses Keccak256\). Use the last 20 bytes of `H`, and add a byte of `0x41` as a prefix. Do a basecheck \(see next paragraph\), and the result will be the final address. All addresses start with 'T'.

Basecheck process: first run SHA256 on the address to get `h1`, then run SHA256 on `h1` to get `h2`. Use the first 4 bytes as a checksum, add it to the end of the address \(`address||check`\). Finally, base58 encode `address||check` to get the final result.

Character map ALPHABET = "123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz"

## Signature <a id="signature"></a>

### Steps <a id="steps"></a>

1. Transfer the `rawdata` of the transaction to `byte[]`.
2. Run SHA256 on the `rawdata`.
3. Use the private key to sign the result of step 2.
4. Add the signature to the transaction.

## Algorithm <a id="algorithm"></a>

ECDSA, SECP256K

### Example <a id="example"></a>

Java

```text
priKey:::8e812436a0e3323166e1f0e8ba79e19e217b2c4a53c970d4cca0cfb1078979df pubKey::04a5bb3b28466f578e6e93fbfd5f75cee1ae86033aa4bbea690e3312c087181eb366f9a1d1d6a437a9bf9fc65ec853b9fd60fa322be3997c47144eb20da658b3d1 hash:::159817a085f113d099d3d93c051410e9bfe043cc5c20e43aa9a083bf73660145 r:::38b7dac5ee932ac1bf2bc62c05b792cd93c3b4af61dc02dbb4b93dacb758123f s:::08bf123eabe77480787d664ca280dc1f20d9205725320658c39c6c143fd5642d v:::0
```

Note: The size of the signature result is 65 bytes:

* `r` = 32 bytes
* `s` = 32 bytes
* `v` = 1 byte
* Full node verifies the signature once receiving a transaction; it generates an address with the value of `hash`, `r`, `s`, and `v`, then it compares with the address in the transaction.

### Demo <a id="demo"></a>

Java

```text
public static Transaction sign(Transaction transaction, ECKey myKey) {    Transaction.Builder transactionBuilderSigned = transaction.toBuilder();    byte[] hash = sha256(transaction.getRawData().toByteArray());    List listContract = transaction.getRawData().getContractList();​    for (int i = 0; i < listContract.size(); i++) {      ECDSASignature signature = myKey.sign(hash);      ByteString bsSign = ByteString.copyFrom(signature.toByteArray());​      //Each contract may be signed with a different private key in the future.      transactionBuilderSigned.addSignature(bsSign);    }  }
```

