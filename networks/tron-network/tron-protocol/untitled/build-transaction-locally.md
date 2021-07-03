# Build transaction locally

This example shows how to build a transaction locally.  
The local transaction construction is used to construct the internal data of the transaction. If the developer has requirements like the offline signature, transaction remarks, Etc, please refer to this article.JSON

```text
message raw {
    bytes ref_block_bytes = 1;//Bytes between 6th and 8th (exclusive) of the latest block height
    int64 ref_block_num = 3;//block height, optional
    bytes ref_block_hash = 4;//Bytes between 8th and 16th (not included) of the hash of the latest block
    int64 expiration = 8;//transaction expiration time，the latest block time + n. Modify n in the configuration file of the local node, the default expiration time of the public node is 1 minute.
  //The condition is (Expiration > latest block time and Expiration < latest block time + 24hrs）.If the conditions are met, the transaction is legal, otherwise the transaction is an expired transaction and will not be accepted by main net.

    repeated authority auths = 9;//permission information
    // data not used
    bytes data = 10;//comments, optional
    //only support size = 1,  repeated list here for extension
    repeated Contract contract = 11;//contract information
    // scripts not used
    bytes scripts = 12;//comments, optional
    int64 timestamp = 14;//transaction created time
    int64 fee_limit = 18;//The trx consuming threshold due to insufficient resources
  }
```

> #### 📘Note：
>
> Currently only RPC interface is supported.

## Java example

Here you can introduce a call environment for the RPC interface via [wallet-cli](https://github.com/tronprotocol/wallet-cli).Java

```text
package org.tron.demo;

import com.google.protobuf.Any;
import com.google.protobuf.ByteString;
import com.google.protobuf.InvalidProtocolBufferException;
import org.tron.api.GrpcAPI.Return;
import org.tron.api.GrpcAPI.TransactionExtention;
import org.tron.common.crypto.ECKey;
import org.tron.common.crypto.Sha256Sm3Hash;
import org.tron.common.utils.ByteArray;
import org.tron.core.exception.CancelException;
import org.tron.protos.Contract;
import org.tron.protos.Protocol.Block;
import org.tron.protos.Protocol.Transaction;
import org.tron.walletserver.WalletApi;

import java.util.Arrays;

public class TransactionSignDemo {
/* Set reference block data*/
  public static Transaction setReference(Transaction transaction, Block newestBlock) {
    long blockHeight = newestBlock.getBlockHeader().getRawData().getNumber();
    byte[] blockHash = getBlockHash(newestBlock).getBytes();
    byte[] refBlockNum = ByteArray.fromLong(blockHeight);
    Transaction.raw rawData = transaction.getRawData().toBuilder()
            .setRefBlockHash(ByteString.copyFrom(ByteArray.subArray(blockHash, 8, 16)))
            .setRefBlockBytes(ByteString.copyFrom(ByteArray.subArray(refBlockNum, 6, 8)))
            .setRefBlockNum(blockHeight)
            .build();
    return transaction.toBuilder().setRawData(rawData).build();
  }

  public static Sha256Sm3Hash getBlockHash(Block block) {
    return Sha256Sm3Hash.of(block.getBlockHeader().getRawData().toByteArray());
  }

  public static String getTransactionHash(Transaction transaction) {
    String txid = ByteArray.toHexString(Sha256Sm3Hash.hash(transaction.getRawData().toByteArray()));
    return txid;
  }

  public static Transaction createTransaction(byte[] from, byte[] to, long amount) {
    Transaction.Builder transactionBuilder = Transaction.newBuilder();
    Block newestBlock = WalletApi.getBlock(-1);
/*设置合约内部数据*/
    Transaction.Contract.Builder contractBuilder = Transaction.Contract.newBuilder();
    Contract.TransferContract.Builder transferContractBuilder =
        Contract.TransferContract.newBuilder();
    transferContractBuilder.setAmount(amount);
    ByteString bsTo = ByteString.copyFrom(to);
    ByteString bsOwner = ByteString.copyFrom(from);
    transferContractBuilder.setToAddress(bsTo);
    transferContractBuilder.setOwnerAddress(bsOwner);
    try {
      Any any = Any.pack(transferContractBuilder.build());
      contractBuilder.setParameter(any);
    } catch (Exception e) {
      return null;
    }
    /* Set memo, transaction expiration time and other data*/
    contractBuilder.setType(Transaction.Contract.ContractType.TransferContract);
    transactionBuilder.getRawDataBuilder().addContract(contractBuilder)
        .setTimestamp(System.currentTimeMillis())
        .setExpiration(newestBlock.getBlockHeader().getRawData().getTimestamp() + 10 * 60 * 60 * 1000)
        .setData(ByteString.copyFromUtf8("memo"))
        .setScripts(ByteString.copyFromUtf8("scripts"));
    Transaction transaction = transactionBuilder.build();
    Transaction refTransaction = setReference(transaction, newestBlock);
    return refTransaction;
  }

  private static byte[] signTransaction2Byte(byte[] transaction, byte[] privateKey)
      throws InvalidProtocolBufferException {
    ECKey ecKey = ECKey.fromPrivate(privateKey);
    Transaction transaction1 = Transaction.parseFrom(transaction);
    byte[] rawdata = transaction1.getRawData().toByteArray();
    byte[] hash = Sha256Sm3Hash.hash(rawdata);
    byte[] sign = ecKey.sign(hash).toByteArray();
    return transaction1.toBuilder().addSignature(ByteString.copyFrom(sign)).build().toByteArray();
  }

  private static boolean broadcast(byte[] transactionBytes) throws InvalidProtocolBufferException {
    return WalletApi.broadcastTransaction(transactionBytes);
  }

  public static void main(String[] args) throws InvalidProtocolBufferException, CancelException {
    String privateStr = "da146374a75310b9666e834ee4ad0866d6f4035967bfc76217c5a495fff9f0d0";
    byte[] privateBytes = ByteArray.fromHexString(privateStr);
    ECKey ecKey = ECKey.fromPrivate(privateBytes);
    byte[] from = ecKey.getAddress();
    byte[] to = WalletApi.decodeFromBase58Check("TN9RRaXkCFtTXRso2GdTZxSxxwufzxLQPP");
    long amount = 100_000_000L; // 100 TRX, api only receive trx in Sun, and 1 trx = 1000000 Sun
    Transaction transaction = createTransaction(from, to, amount);
    byte[] transactionBytes = transaction.toByteArray();
    byte[] transaction4 = signTransaction2Byte(transactionBytes, privateBytes);
    boolean result = broadcast(transaction4);

    System.out.println(result);
  }
}
```

After executing the above code, the result of querying this transaction information.gettransactionbyid

```text
{
    "ret": [
        {
            "contractRet": "SUCCESS"
        }
    ],
    "signature": [
        "ced3929af13ca455fca59088c1a98908897640f6dc7c5746f1a21eb850fb266e6d7996e1984464b0d8a262f991342a1c9e4197311ea3562631f411ffde9abcda00"
    ],
    "txID": "a1185aad04cfa78cb66d5eb3780b8801dde1d49d14aee9e21841194b81a64bd6",
    "raw_data": {
        "data": "6d656d6f",
        "contract": [
            {
                "parameter": {
                    "value": {
                        "amount": 100000000,
                        "owner_address": "41bf97a54f4b829c4e9253b26024b1829e1a3b1120",
                        "to_address": "41859009fd225692b11237a6ffd8fdba2eb7140cca"
                    },
                    "type_url": "type.googleapis.com/protocol.TransferContract"
                },
                "type": "TransferContract"
            }
        ],
        "ref_block_bytes": "c75b",
        "ref_block_hash": "7cfc890c6e4d7a15",
        "expiration": 1583304414000,
        "ref_block_num": 2541403,
        "scripts": "73637269707473",
        "timestamp": 1583268416080
    },
    "raw_data_hex": "0a02c75b18db8e9b0122087cfc890c6e4d7a1540b0a6b0a28a2e52046d656d6f5a68080112640a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412330a1541bf97a54f4b829c4e9253b26024b1829e1a3b1120121541859009fd225692b11237a6ffd8fdba2eb7140cca1880c2d72f62077363726970747370d0949b918a2e"
}
```

> #### 📘Note：
>
> The information in the data field can be used as memo information \(the data is displayed in TronScan\), and the content is retrieved by Hex to String.

