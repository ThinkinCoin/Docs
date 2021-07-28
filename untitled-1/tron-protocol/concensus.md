# Concensus

Blockchain is a distributed accounting system. There can be thousands of nodes in a blockchain system, each independently storing the same ledger. If new transaction data is to be written into the ledger, approvals from these nodes are needed. Achieving this goal in an untrusted distributed environment is a complicated systematic quest. The blockchain system operates normally means each node in the blockchain can always keep the same ledger, provided that most nodes in the system are honest and reliable. In order to ensure that honest and reliable nodes can jointly supervise the transaction data written into the ledgers, each blockchain system needs to build its consensus, which is equivalent to the constitution of the blockchain. As long as the vast majority of nodes comply with the consensus requirements, it can guarantee that the results will undoubtedly be credible, even in an untrusted distributed environment. Therefore, the consensus is an agreement that honest nodes achieve to maintain the stability of the blockchain.

Different blockchain systems will have a unique way of implementation. There are several types of consensus, and the most commonly used are POW, POS, and DPoS. This article will mainly introduce the DPoS consensus on which TRON based. We will also explain the essential components and mechanisms of DPoS.

## Block Producing Process <a id="block-producing-process"></a>

The witnesses of the blockchain network collect the newly generated transactions in the blockchain network and verify the legality of these transactions, then package the transactions in a block, record them as a new page on the ledger, and broadcast the page to the entire blockchain network. Next, other nodes will receive the new page and verify the legality of the transaction data on the page and add it to their ledger. Finally, the witnesses will repeat this process so all new transaction data in the blockchain system can be recorded in the ledger.

## DPoS Overview <a id="dpos-overview"></a>

The role of consensus is to select the witnesses in the blockchain system. The witnesses verify the transaction data, keep the account to broadcast new accounts to other nodes in the network, and obtain the approval of the new accounts from other nodes. As a specific implementation of consensus, DPoS works in the following way:

The DPoS consensus selects some nodes as witnesses in the blockchain system based on the number of votes they receive. First, when the blockchain system starts to operate, a certain number of tokens will be issued, and then the tokens will be given to nodes in the blockchain system. Then, a node can apply to be a witness candidate in the blockchain system with a portion of the tokens. Any token-holding node in the blockchain system can vote for these candidates. Every t period, the votes for all the candidates will be counted. Top N candidate nodes with the most votes will become witnesses for the following t period. After t period, the votes will be counted again to elect the new witnesses, and the cycle continues.

Let us see how it's realized in the context of TRON:

## Definition <a id="definition"></a>

* TRON: refers to the TRON network. The document does not distinguish between TRON, TRON blockchain, TRON blockchain system, etc.
* TRON token: refers to the equity token issued by and circulating in TRON, known as TRX.
* Witnesses candidates: nodes eligible for becoming witnesses in TRON.
* Witnesses: nodes in TRON qualified for book-keeping. They are usually called witnesses in DPoS. There will be 27 witnesses in TRON, which are also called super nodes \(or SR\). Here, we will not distinguish between a bookkeeper, witness, supernode, SR, Etc.
* Bookkeeping: The process of verifying transactions and recording them in a ledger. Because blocks carry ledgers in TRON, the bookkeeping process is also called block generation. We will not distinguish between bookkeeping and block generation in the document.
* Bookkeeping order: block generation order. The descending order of the 27 witnesses based on the number of votes they receive.
* Block time: TRON sets block time to be 3 seconds. This means a block is generated every 3 seconds.
* Slot: after each block is generated, it can be put into a slot, and each block will take up a slot. For example, there are 20 slots for every minute. When a block is generated during the block time, the corresponding slot will be filled. However, if a block is not generated, then the corresponding slot will be empty. The next block generated will fill in a new corresponding slot.
* Epoch: TRON sets an Epoch to be 6 hours. The last two block time of an Epoch is the maintenance period, during which the block generating orders for the next Epoch will be decided.
* Maintenance period: TRON sets the period to be two block time, which is 6 seconds. This period is used to count the votes for candidates. There are 4 Epochs in 24 hours, and naturally, four maintenance periods. Witnesses pause to produce block during the maintenance period. The block generation order for the next epoch will be decided in the maintenance period.

​![](https://files.readme.io/2c7fd14-61624595420_.pic.jpg)​![](https://files.readme.io/2c7fd14-61624595420_.pic.jpg)​

## Election Mechanism <a id="election-mechanism"></a>

1. Votes

In TRON, 1 TRX equals one vote.

1. Voting process

In TRON, voting for candidates is a special transaction. Nodes can vote for candidates by generating a voting transaction.

1. Vote counting

During each maintenance period, the votes for candidates will be counted. The top 27 candidates with the most votes will be the witnesses for the next Epoch.

## Block generation mechanism <a id="block-generation-mechanism"></a>

During each Epoch, the 27 witnesses will take turns to generate blocks according to the bookkeeping order. Each witness can only generate blocks when it is their turn. Witnesses package the data of multiple verified transactions into each block. The witness will sign the data of this block with their private key and fill witness\_signature, address of the witness, the block height, the time that block is generated, Etc into the block. The hash of the previous block will be included in each new block as the parent Hash.

Through storing the hash of the previous block, blocks are logically connected. Eventually, they form a chain. A typical blockchain structure is shown in the following picture:![](https://files.readme.io/8a88caa-31624594014_.pic.jpg)​![](https://files.readme.io/8a88caa-31624594014_.pic.jpg)​

In ideal circumstances, the bookkeeping process in a DPoS consensus-based blockchain system proceeds according to the bookkeeping order calculated in advance. Witnesses generate blocks in turn \(see figure a\). However, the blockchain network is a distributed and untrusted complex system in the following three ways.

* Due to a poor network environment, blocks generated by some witnesses cannot be received by other witnesses at an invalid time \(see figure b1 and b2\).
* The normal operation of a certain witness cannot always be guaranteed \(see figure c\).
* Some malicious witnesses will generate fork blocks in order to fork the chain \(see figure d\).

​![](https://files.readme.io/a595076-71624595529_.pic.jpg)​![](https://files.readme.io/a595076-71624595529_.pic.jpg)​![](https://files.readme.io/de89f88-81624595552_.pic.jpg)​![](https://files.readme.io/de89f88-81624595552_.pic.jpg)​

As mentioned above, the basis for the blockchain system to operate normally is that most of the nodes in the system are honest and reliable. Furthermore, the primary guarantee for the security of the blockchain system is the ledger's security, meaning that illegal data cannot be written into the ledger maliciously, and ledger copies saved on each node should be consistent. Based on the DPoS consensus, the bookkeeping process is carried out by witnesses. Therefore, the safety of TRON depends on the reliability of the majority of the witnesses. TRON has put confirmed blocks in the system which are irreversible. At the same time, to resist the malicious behaviours of a small number of witness nodes, TRON recognizes the longest chain as the main chain based on "the longest chain principle".

**The confirmed block principle**

The newly produced blocks are unconfirmed. Only those blocks that are "approved" by more than 70% \(i.e. 27 \* 70% = 19, rounded up\) of the 27 Witnesses are considered irreversible blocks, commonly referred to as solidified blocks. The entire blockchain network has confirmed the transactions contained in the solidified blocks. The way to "approve" the unconfirmed state block is that witness producing subsequent blocks after it. The point to be emphasized here is that the Witnesses producing these 18 blocks must be different from each other and the Witnesses producing the 103rd block.

**The longest chain principle**

When a fork occurs, an honest witness would always choose to produce blocks on the longest chain.

## Incentive Model <a id="incentive-model"></a>

TRON sets up an incentive model to encourage node participation and network expansion to ensure the safe and efficient operation of the blockchain system. Witnesses who complete block production tasks will be rewarded with TRX. The model also specifies that for every confirmed block produced by a witness, the witness will receive 32 TRX. In addition, the first 127th witnesses \(including witness candidates\) with the most votes will receive proportional rewards during the maintenance period of each Epoch.

## Proposal-based Parameter Adjustment <a id="proposal-based-parameter-adjustment"></a>

A notable characteristic of DPoS is that any parameter adjustment can be proposed on the chain, and witnesses will decide whether to approve the proposal by starting a vote. The advantage of this method is that it avoids hard fork upgrades when adding new features. Currently, TRON supports the following parameter adjustments:

Refer to [Tronscan](https://tronscan.org/#/sr/committee) for the parameter details.

## Appendix: Reference Documentations <a id="appendix-reference-documentations"></a>

* * * * 
