# Introduction

## What is TRON <a id="what-is-tron"></a>

TRON is a robust blockchain ecosystem designed and developed by blockchain developers over the world, which follows the philosophy of "Decentralize the Web". There are multiple kinds of products involved in TRON ecosystem, including public chain, wallet client, decentralized applications\(DAPPs\), Etc. These products are closely related to each other, and together, this supports the stability of the whole ecosystem.

## TRON Public Chain <a id="tron-public-chain"></a>

### 1.Overview <a id="1-overview"></a>

TRON public chain is a decentralized blockchain network implemented based on TRON protocol, performs as the core of TRON ecosystem, launched on Jun 25th 2018. Many things can be done through TRON public chain, including token assets issuing, DAPP deployment and running, stake and vote for gains, assets transferring, Etc.

TRON public chain is one of the most secure public chain systems at present. The reason it is outstanding is that the blockchain runs in a decentralized network environment, in which creation and storage of the data do not rely on specific individuals or organizations, and the data is ensured to be never changed by cryptography.

TRON public chain has better operational efficiency and stability than most public chains due to a well-designed architecture and code.

### 2.Present <a id="2-present"></a>

TRON ecosystem has set itself a 10-year roadmap in the original [TRON whitepaper](https://dn-peiwo-web.qbox.me/Tron-Whitepaper-0822-V17.pdf):

* Exudos 2017.8~2018.12
* Odyssey 2019.1~2020.6
* Great Voyage 2020.7~2021.7
* Apollo 2021.8~2023.3
* Star Trek 2023.4~2025.9
* Eternity 2025.4~2027.9

The design for the top-level of the system and protocols of the public chain was made in Exudos.

Odyssey is an essential stage of the large-scale practical development of the TRON public chain. There are some key versions, including:

* TRON public chain \(test net version\) [Odyssey-v1.0](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v1.0)​
* TRON public chain \(main net version\) [Odyssey-v2.0](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v2.0)​
* TRON Virtual Machine\(TVM\), making Ethereum smart contracts fully compatible [Odyssey-v3.0](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v3.0)​
* In-memory database for accessing TRON public data [Odyssey-v3.2](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v3.2)​
* Supporting multi-signature and account authority management [Odyssey-v3.5](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v3.5)​
* Adding RocksDB as a new underlying data engine [Odyssey-v3.5.1](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v3.5.1)​
* New decentralized incentive mechanism [Odyssey-v3.6.5](https://github.com/tronprotocol/java-tron/releases/tag/Odyssey-v3.6.5)​
* New consensus mechanism TPos[Great Voyage-v4.0](https://github.com/tronprotocol/java-tron/tree/release_4.0)​

The development of TRON public chain has reached the stage of the Great Voyage.

### 3. Architecture <a id="3-architecture"></a>

TRON public chain realizes the design of highly abstract modularisation. It separates the system into several core modules, including underlying network, data storage, consensus, transaction actuator, TVM, and application layer interface.

​[TRON Public chain architecture](https://dn-peiwo-web.qbox.me/Design_Book_of_TRON_Architecture1.4.pdf)​

#### Underlying network <a id="underlying-network"></a>

The underlying network module is a set of customizable and efficient message response systems, built based on Netty, a high-performance network framework.

The underlying network module is separated into two modules: node communication and node discovery.

Node discovery is implemented based on the Kademlia algorithm. It meets the requirements of node discovery in decentralized network environments and can defend eclipse and witch attacks by a set of node scoring mechanism.

The node communication module uses TCP for data transfer. Based on this, a flexible and extensible message registration response mechanism is designed on the business layer.

#### Data storage <a id="data-storage"></a>

We have designed a data storage module that can support fast rollback and an in-memory database KhaosDB for fast blockchain switching. These reflect the ultimate pursuit of the performance of the TRON public chain.

We also published ChainBase, a database product for the blockchain system, based on the excellent interface design of the data storage module. It supports the switching of data engines between LevelDB and RocksDB as well as the customized development of data engines, only needed to implement the corresponding interface set.

​[ChainBase](https://github.com/tronprotocol/chainbase)​

#### Consensus <a id="consensus"></a>

TRON public chain currently adopts DPOS as the consensus algorithm, which enables a maximum 2000 TPS.

Blocks are categorized as solidified and un-solidified block to tap the performance potential of the public chain. It can reduce the limits of the CAP theory of distributed systems and give the most consideration to data availability and consistency.

Solidified blocks cannot be rolled back. Un-solidified blocks contain the latest transaction data. Full nodes provide data inquiry services for both types of blocks to meet various needs from users.

We have designed an excellent on-chain governance mechanism that attributes to the implementation of the DPOS algorithm. Super Representatives \(SRs\) and Super Representative Partners \(SRPs\) can initiate voting requests for proposals. After voting, all votes from SRs are counted to determine whether a proposal takes effect.

A proposal can include adjustments of blockchain parameters, the opening of new features, etc. Proposal mechanism can prevent a node from multiple restarts during a blockchain update, which improves the efficiency of the consensus and provides a channel for community supervision.

​[Super Representatives](https://developers.tron.network/docs/super-representatives)​

​[TRON consensus mechanism DPOS](https://tronprotocol.github.io/documentation-zh/introduction/dpos/)​

#### On-chain governance & incentive mechanism <a id="on-chain-governance-and-incentive-mechanism"></a>

Through the decentralized election, TRON public chain produces two types of roles: Super Representative \(SR\) and Super Representative Partner\(SRP\), and they participate in the on-chain governance. An SR/ SRP can initiate votings for specific proposals, and other SRs/ SRPs can give their opinions to the proposals through voting, which ensures the blockchain governance is entirely decentralized.

TRON public chain has a precise and efficient incentive mechanism that can promote the self-prosperity of the blockchain. SRs have the power of packing transactions, producing blocks and obtaining block production incentives. SRs and SR partners gain awards based on the votes they get, and at the same time, ordinary voters can earn stake reward for voting SRs and SRPs. The amount of incentive is transparent, and the distribution process is entirely decentralized.

​[Incentive Mechanism](doc:%E8%B6%85%E7%BA%A7%E4%BB%A3%E8%A1%A8%E5%92%8C%E6%9C%BA%E5%88%B6)​

#### TaPoS <a id="tapos"></a>

Double spend attack has always been the issue that needs to be treated strictly in the history of the public blockchain. TRON has the TaPos mechanism to defend this kind of attacks, which improves the safety of TRON public chain.

#### TRC10 token support <a id="trc10-token-support"></a>

TRC10 token is based on system contracts, can be issued simply on TRON public chain. TRC10 standard significantly reduces the cost of token circulation, as system contract transactions only consume bandwidth. TRC10 token transactions can be done in the decentralized exchange built in TRON public chain.

​[TRC10](https://developers.tron.network/docs/trc10)​

#### TVM and smart contracts <a id="tvm-and-smart-contracts"></a>

TRON Virtual Machine\(TVM\) implemented in TRON public chain is fully compatible with the Ethereum Virtual Machine\(EVM\). Not only does TVM reduce the learning cost for developers, due to the born advantage of DPOS consensus algorithm of TRON public chain, but also improves operational efficiency and reduces the cost.

We have made many optimizations on TVM to reduce the cost of the operational cost of DAPPs. Also, we develop a lot of new features to support more business logic in smart contracts, including batch signature verification, contract address judgment, etc.

​[TVM overview](https://en.developers.tron.network/docs/virtual-machine-introduction)​

​[Getting started to DAPP development](https://en.developers.tron.network/docs/introduction)​

#### Resource model <a id="resource-model"></a>

TRON public chain has an excellent resource model. We have designed a dynamic adjustment mechanism for resource model parameters, which is useful for feedback regulation. The brief explanation of this mechanism is the number of processing transactions is positively correlated with the resource fee.

Every user has a certain amount of free resource quota.

Users can freeze their TRX to acquire free bandwidth/energy and a corresponding amount of votes. Voting for SRs will be rewarded base on the voting volume.

​[Resource model](https://cn.developers.tron.network/docs/%E8%B5%84%E6%BA%90%E6%A8%A1%E5%9E%8B)​

## Core applications in TRON ecosystem <a id="core-applications-in-tron-ecosystem"></a>

### 1.Overview <a id="1-overview-1"></a>

TRON public chain is a large-scale distributed operating system, having tens of thousands of nodes running on service, and terminals are all over the world. Like Office to Microsoft, the power of TRON public chain cannot be separated from the support of application software, and the prosperity of TRON's ecosystem needs community developers to work together.

There are many brilliant software in TRON ecosystem at present.

### 2.Wallet client <a id="2-wallet-client"></a>

#### Wallet-Cli <a id="wallet-cli"></a>

Wallet-Cli is the official wallet client maintained by TRON Foundation.

Wallet-Cli is a command-line version of the wallet, provides essential tools to communicate with the TRON public chain by the RPC protocol, supports all functions of the TRON public chain in real-time.

Wallet-Cli is also an excellent code implementation to show the interactive mode between clients and the blockchain for developers.

​[Wallet-Cli](https://github.com/tronprotocol/wallet-cli)​

#### TronLink <a id="tronlink"></a>

TronLink is an outstanding TRON wallet dedicated to providing users with complete functions, convenient experience, secure funding options, and the most applications.

​[TronLink official website](https://www.tronlink.org/)​

​[Tronlink intergration](https://en.developers.tron.network/docs/tronlink%E9%9B%86%E6%88%90)​

### 3.Blockchain explorer <a id="3-blockchain-explorer"></a>

tronscan.org is the first blockchain explorer based on TRON.

tronscan.org has all the essential functions of a blockchain explorer, including searching transactions/ accounts/ blocks/ nodes/ smart contracts, on-chain statistics, token creation, Etc.

tronscan.org also has a built-in web wallet and a DEX based on the Bancor protocol, and they enrich the application matrix of Tronscan.

​[Tronscan](https://tronscan.org/#/)​

### 4.DAPP <a id="4-dapp"></a>

TRON public chain has attracted tens of thousands of community developers to join in the development, deployment, and running of DAPPs on the blockchain, for the reason of its high performance, safety, and low cost.

As of Q1 of 2020, the total number of DAPPs on the TRON public chain has exceeded 700, with more than 230,000 users.

### 5.Testnet <a id="5-testnet"></a>

**Shasta test net**

The version of Shasta test net is consistent with the main net.

* * * * TronGrid API / Full Node API / Event API: [https://api.shasta.trongrid.io](https://api.shasta.trongrid.io/)​
* * gRPC: grpc.shasta.trongrid.io:50051

**Nile test net**

Nile test net is generally used to test new features. The code version of the Nile test net is ahead of the main net as usual.

* Official website: [https://nileex.io/](https://nileex.io/)​
* * * * * * Public full node:

  47.252.19.181 47.252.3.238

* 
**Tronex test net**

Tronnex is used for the test of sun-network.

* * * * * * * Public full node:

  47.252.87.28

  47.252.85.13

* 
## TRON's ecosystem growth <a id="trons-ecosystem-growth"></a>

The healthy growth of TRON's ecosystem can never be separated from ecological products. The products under development and testing are listed here:

* Lite client

  A full node will be more accessible to devices with lower specs.

* Lite full node

  It solves the problem of the massive data occupation of a full node. A lite full node can provide service like a full node but only stores a fraction of data

* Support shielded transaction on the TRON public chain

  It provides more security functions for data.

* TronDex

  It is an optimization of the current DEX, which supports TRC10 automatic transaction matching and TRC20 decentralized transaction.

* Sidechain based on Sun Network

  It is a DAPPchain based on Sun Network and it attracts more DAPP developers to deploy their blockchain.

* The mixture of PBFT and DPOS

  It is getting ready for the coming cross-chain implementation.

We have countless star products from the community:

* ​[TRONZ supports shielded transaction](http://tronz.io/)​

  TRONZ is currently doing the MPC process. The shielded coin based on the TRON public chain will be published after the process done

* * DeFi\(decentralized finance\)

  The first staking and lending platform [JUST](https://just.tronscan.org/#)​

  The TRX staked on JUST is over 1,000,000,000, has exceeded the similar product MakerDAO

* Developer tools

  ​[TronWeb](doc:%E5%85%A5%E9%97%A8-1) provides the JS front-end tool code for communicating with the blockchain

  ​[TronIDE](doc:%E5%85%A5%E9%97%A8-2) provides an integrated tool of editing, deploying testing and calling of smart contracts

  ​[TronGrid](doc:trongrid%E5%85%A5%E9%97%A8) provides full node and extra API services

* TronLink

  TrokLink is a great TRON wallet developed by the community, runs on Android, IOS and PCs\(Chrome extension\). It is a vital entrance of DAPPs.

  TronLink has more than 300,000 users at present.

## The future of TRON <a id="the-future-of-tron"></a>

We are always adhering to the concept of "haste makes waste" over the past two years from the day we began to build the ecosystem. Looking back, we did many things. At present, our core public chain product "java-tron" is keeping in stable operation. Besides, many brilliant products and ideas, like wallet clients, blockchain explorers, side chains based on Sun network, different kinds of DAPPs and our outstanding community developers are the most important part which forms TRON ecosystem today.

In the future, we will adhere to the value concept of "decentralized the web" and keep on going in the following areas:

* Cross-chain based on the TRON public chain
* Full support for shielded transactions
* A safer and faster TVM
* Integrate with other products like BTFS, bring more application scenarios to DAPPs
* Exploration in DeFi area

