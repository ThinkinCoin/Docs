# Build transaction locally

package org.tron.demo;

​

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

​

import java.util.Arrays;

​

public class TransactionSignDemo {

/\* Set reference block data\*/

 public static Transaction setReference\(Transaction transaction, Block newestBlock\) {

 long blockHeight = newestBlock.getBlockHeader\(\).getRawData\(\).getNumber\(\);

 byte\[\] blockHash = getBlockHash\(newestBlock\).getBytes\(\);

 byte\[\] refBlockNum = ByteArray.fromLong\(blockHeight\);

 Transaction.raw rawData = transaction.getRawData\(\).toBuilder\(\)

 .setRefBlockHash\(ByteString.copyFrom\(ByteArray.subArray\(blockHash, 8, 16\)\)\)

 .setRefBlockBytes\(ByteString.copyFrom\(ByteArray.subArray\(refBlockNum, 6, 8\)\)\)

 .setRefBlockNum\(blockHeight\)

 .build\(\);

 return transaction.toBuilder\(\).setRawData\(rawData\).build\(\);

 }

​

 public static Sha256Sm3Hash getBlockHash\(Block block\) {

 return Sha256Sm3Hash.of\(block.getBlockHeader\(\).getRawData\(\).toByteArray\(\)\);

 }

​

 public static String getTransactionHash\(Transaction transaction\) {

 String txid = ByteArray.toHexString\(Sha256Sm3Hash.hash\(transaction.getRawData\(\).toByteArray\(\)\)\);

 return txid;

 }

​

 public static Transaction createTransaction\(byte\[\] from, byte\[\] to, long amount\) {

 Transaction.Builder transactionBuilder = Transaction.newBuilder\(\);

 Block newestBlock = WalletApi.getBlock\(-1\);

/\*设置合约内部数据\*/

 Transaction.Contract.Builder contractBuilder = Transaction.Contract.newBuilder\(\);

 Contract.TransferContract.Builder transferContractBuilder =

 Contract.TransferContract.newBuilder\(\);

 transferContractBuilder.setAmount\(amount\);

 ByteString bsTo = ByteString.copyFrom\(to\);

 ByteString bsOwner = ByteString.copyFrom\(from\);

 transferContractBuilder.setToAddress\(bsTo\);

 transferContractBuilder.setOwnerAddress\(bsOwner\);

 try {

 Any any = Any.pack\(transferContractBuilder.build\(\)\);

 contractBuilder.setParameter\(any\);

 } catch \(Exception e\) {

 return null;

 }

 /\* Set memo, transaction expiration time and other data\*/

 contractBuilder.setType\(Transaction.Contract.ContractType.TransferContract\);

 transactionBuilder.getRawDataBuilder\(\).addContract\(contractBuilder\)

 .setTimestamp\(System.currentTimeMillis\(\)\)

 .setExpiration\(newestBlock.getBlockHeader\(\).getRawData\(\).getTimestamp\(\) + 10 \* 60 \* 60 \* 1000\)

 .setData\(ByteString.copyFromUtf8\("memo"\)\)

 .setScripts\(ByteString.copyFromUtf8\("scripts"\)\);

 Transaction transaction = transactionBuilder.build\(\);

 Transaction refTransaction = setReference\(transaction, newestBlock\);

 return refTransaction;

 }

​

 private static byte\[\] signTransaction2Byte\(byte\[\] transaction, byte\[\] privateKey\)

 throws InvalidProtocolBufferException {

 ECKey ecKey = ECKey.fromPrivate\(privateKey\);

 Transaction transaction1 = Transaction.parseFrom\(transaction\);

 byte\[\] rawdata = transaction1.getRawData\(\).toByteArray\(\);

 byte\[\] hash = Sha256Sm3Hash.hash\(rawdata\);

 byte\[\] sign = ecKey.sign\(hash\).toByteArray\(\);

 return transaction1.toBuilder\(\).addSignature\(ByteString.copyFrom\(sign\)\).build\(\).toByteArray\(\);

 }

​

 private static boolean broadcast\(byte\[\] transactionBytes\) throws InvalidProtocolBufferException {

 return WalletApi.broadcastTransaction\(transactionBytes\);

 }

​

 public static void main\(String\[\] args\) throws InvalidProtocolBufferException, CancelException {

 String privateStr = "da146374a75310b9666e834ee4ad0866d6f4035967bfc76217c5a495fff9f0d0";

 byte\[\] privateBytes = ByteArray.fromHexString\(privateStr\);

 ECKey ecKey = ECKey.fromPrivate\(privateBytes\);

 byte\[\] from = ecKey.getAddress\(\);

 byte\[\] to = WalletApi.decodeFromBase58Check\("TN9RRaXkCFtTXRso2GdTZxSxxwufzxLQPP"\);

 long amount = 100\_000\_000L; // 100 TRX, api only receive trx in Sun, and 1 trx = 1000000 Sun

 Transaction transaction = createTransaction\(from, to, amount\);

 byte\[\] transactionBytes = transaction.toByteArray\(\);

 byte\[\] transaction4 = signTransaction2Byte\(transactionBytes, privateBytes\);

 boolean result = broadcast\(transaction4\);

​

 System.out.println\(result\);

 }

}

