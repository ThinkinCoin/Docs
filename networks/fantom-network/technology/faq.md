# FAQ

This guide addresses as many questions you might have about Fantom as possible. Please refer to this FAQ section before asking questions on Discord. If your question is still unanswered, please reach out to us through the chat function on our [website](https://fantom.foundation/) in the bottom right corner or join our [Discord](http://chat.fantom.network/).

​[General questions](faq.md#general-questions) [FTM token](faq.md#ftm-token) [Opera network](faq.md#opera-network) [Tools](faq.md#tools)​

## General questions <a id="general-questions"></a>

### What is a consensus algorithm? <a id="what-is-a-consensus-algorithm"></a>

A consensus algorithm is a mechanism to reach agreement among nodes in distributed networks. It removes the need for a central authority and allows the whole network to agree on data and the ordering of events in a trustless way.

Nodes participating in the network maintain an exact copy of the ledger, allowing applications built on top of the consensus protocol to function correctly.

### What is aBFT \(asynchronous Byzantine Fault Tolerant\) consensus? How is it different from blockchains such as Ethereum and Bitcoin? <a id="what-is-abft-asynchronous-byzantine-fault-tolerant-consensus-how-is-it-different-from-blockchains-such-as-ethereum-and-bitcoin"></a>

aBFT consensus stands for “asynchronous Byzantine Fault Tolerant” consensus. When a network is said to be “Byzantine Fault Tolerant”, it means that nodes can still reach an agreement on an ordering of events even if part of the network acts maliciously.

Asynchronous BFT allows nodes in the network to confirm event blocks containing transactions without depending on any timing assumptions. This makes the confirmation of transactions by the network faster, without compromising security or decentralization. When a transaction is confirmed by the network, it achieves complete finality and can’t be changed nor reverted. aBFT consensus reaches agreement on transactions even when some of the messages between nodes are lost, which makes the network more resilient

Blockchains such as Ethereum and Bitcoin are synchronous, meaning that transactions are appended into blocks, one at a time. They follow the longest-chain rule in which the chain with the most number of blocks determines the final ordering of events. Transactions in earlier blocks have a much higher probability of being part of the final ordering of events compared to more recent transactions. Therefore, these networks require multiple confirmations to ensure that a transaction is permanently part of the blockchain. This behavior leads to a slower confirmation of the transactions than in aBFT consensus.

### What is finality? <a id="what-is-finality"></a>

Finality means that a transaction cannot be changed or reversed by any party. aBFT consensus algorithms such as Lachesis have a very low time to finality because they achieve absolute finality. Absolute finality means that a transaction is considered final once it is included in a block.

In the case of Fantom, Opera Chain can accomplish finality in 1 to 2 seconds. TxFlow can achieve finality in less than a second.

Conversely, Nakamoto consensus protocols rely on probabilistic finality. In this case, the probability that a transaction won’t be reverted increases with time. The more blocks that are created on top of a block, thereby confirming it as correct, the more difficult and costlier it would be to revert a transaction in that block. At some point it becomes theoretically impossible to alter older blocks, increasing the probabilistic finality to near 100%.

Bitcoin has finality of 30 to 60 minutes; when using Bitcoin you have to wait a few block confirmations before considering the transaction final and irreversible. Ethereum has a finality of a few minutes.

### What is TxFlow? <a id="what-is-txflow"></a>

TxFlow is an aBFT middleware protocol designed for responsiveness. It runs together with a traditional consensus algorithm such as Lachesis, which guarantees network security.

TxFlow can achieve sub-second latency, which makes it ideal for any application that requires instant confirmation. Check the [GitHub](https://github.com/Fantom-foundation/go-txflow) and the TxFlow [introduction](https://medium.com/fantomfoundation/introducing-txflow-the-protocol-for-responsiveness-a2e42bd5fc3c)​

## FTM token <a id="ftm-token"></a>

### Is FTM an ERC20 token? <a id="is-ftm-an-erc20-token"></a>

Fantom has an ERC20 token, but it can’t be used directly on the Opera mainnet. When you send your ERC-20 to the [Fantom Wallet](https://fantom.foundation/ftm-wallet/), it will automatically be swapped to Opera FTM.

Here’s a breakdown of the different FTM tokens in circulation at the moment

1. Opera FTM: Used on Fantom’s mainnet Opera Chain 2. ERC20: Exists on the Ethereum network 3. BEP2: Exists on Binance Chain

Note that Fantom Opera addresses share the same structure as Ethereum addresses \(0x…\), **but they are not Ethereum addresses**.

### Can I send ERC20 FTM tokens to my Fantom Wallet? <a id="can-i-send-erc20-ftm-tokens-to-my-fantom-wallet"></a>

Yes. On the “Receive” tab of your Fantom wallet just pick Ethereum and send your tokens to the displayed address. Your tokens will be automatically swapped to Opera FTM which allow you to stake and vote.

### What’s the purpose of the FTM token? <a id="whats-the-purpose-of-the-ftm-token"></a>

The FTM token has a number of use cases within the Fantom ecosystem. It plays an essential role for a well-functioning, healthy network.

**1. Securing the network**

Fantom uses a Proof-of-Stake system that requires validators to hold FTM. Anyone with at least 3,175,000 FTM can run their own validator node to earn epoch rewards and transaction fees. Every FTM holder has the option to delegate their tokens to a validator \(while keeping full custody of their funds\) to receive staking rewards. Validators then take a small fee for their services.

By locking in their FTM, validators help the network to be decentralized and secure.

**2. Paying for network fees** To compensate validators for their services and prevent transaction spam, every action performed within the Fantom network costs a small fee. This fee is paid in FTM.

**3. Voting in on-chain governance** Decisions regarding the Fantom ecosystem are made using transparent on-chain voting. Votes are weighted according to the amount of FTM held by an entity. Basically, 1 FTM equals 1 vote.

With FTM as the governance token, validators and delegators can vote on network parameters such as block rewards as well technical committees and so forth.

**4. Additional use cases** FTM is used as a collateral on the Fantom DeFi suite, [Fantom Finance](https://fantom.foundation/defi/).

### How can I stake FTM? <a id="how-can-i-stake-ftm"></a>

Check out [this guide](../staking/stake-on-fantom.md).

### Can I stake FTM on exchanges like Binance? <a id="can-i-stake-ftm-on-exchanges-like-binance"></a>

You can’t stake FTM on exchanges at the moment.

### How to run a validator on Opera? <a id="how-to-run-a-validator-on-opera"></a>

To run a validator node on Fantom’s Opera Chain, the followings are required:

1. A minimum stake of 3,175,000 FTM;
2. AWS EC2 m5.large instance \(or equivalent\) and ~800GB of disk storage \(or equivalent\) as the minimum recommended hardware specifications.

​[Step-by-step guide](../staking/run-a-validator-node.md)​

### Where can I store FTM? <a id="where-can-i-store-ftm"></a>

You can store Opera FTM on our official [PWA wallet](https://pwawallet.fantom.network/#/) for mobile and desktop.

Visit [https://fantom.foundation/how-to-use-fantom-wallet/\#installing-wallet/](https://fantom.foundation/how-to-use-fantom-wallet/#installing-wallet/) for a guide on how to use it.

Please note that the above wallets only support Opera Network FTM. They do not support ERC20 or BEP2.

We are working with other wallet providers to add compatibility for the FTM token.

## Opera network <a id="opera-network"></a>

### What is Opera? <a id="what-is-opera"></a>

Opera is a fully decentralized blockchain network with smart contracts integration for applications. It is compatible with the Ethereum Virtual Machine and powered by Fantom’s aBFT consensus. Thus, smart contracts developed on Ethereum can run on Opera, with an increase of scalability and security.

### Is Fantom compatible with Ethereum smart contracts? <a id="is-fantom-compatible-with-ethereum-smart-contracts"></a>

Yes. Fantom’s Opera Network is fully compatible with the Ethereum Virtual Machine \(EVM\). It also has Web3JS API and RPC support. All smart contracts written in Solidity or Vyper, compiled and deployed on Ethereum, are fully compatible with the Opera Network.

Fantom is currently working with both the University of Sydney Programming Languages group, and the Yonsei University Embedded System Languages and Compilers Group, to build a new “Fantom Virtual Machine” \(FVM\), interpreter, and database to achieve much better performance and security than the EVM. The FVM will be compatible with the Solidity programming language.

### Is Fantom compatible with Cosmos SDK? <a id="is-fantom-compatible-with-cosmos-sdk"></a>

Yes. Developers can use Fantom’s uber-fast and secure aBFT consensus mechanism as a base layer and use the Cosmos SDK on top of it.

### What programming languages does Fantom support? <a id="what-programming-languages-does-fantom-support"></a>

Fantom’s Opera network supports all smart contract languages that Ethereum supports for the EVM, which include both Solidity and Vyper.

### When did Fantom mainnet go live? <a id="when-did-fantom-mainnet-go-live"></a>

The Fantom Opera Chain went live on 27 December 2019.

### How is Fantom governed? What does on-chain governance look like? <a id="how-is-fantom-governed-what-does-on-chain-governance-look-like"></a>

The Fantom Foundation is currently in charge of the governance of the network, advised by the community and validator nodes. We plan to launch a governance smart contract that will allow validators and token holders to determine the direction of Fantom, as well as to approve changes to the underlying consensus via hard and soft forks.

Find out [more details on Fantom’s governance proposal](https://github.com/Fantom-foundation/FIPs/blob/master/FIPS/governance.pdf).

* * 

