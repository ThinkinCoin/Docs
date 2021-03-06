# Dapps

A dapp is a service that enables direct interaction between end users and providers \(e.g. connecting buyers and sellers in some marketplace, owners and storers in file storage\). Ethereum dapps typically interface users via an HTML/Javascript web application using a Javascript API to communicate with the blockchain. Dapps would typically have their own suite of associated contracts on the blockchain which they use to encode business logic and allow persistent storage of their consensus-critical state. Remember that because of the redundant nature of computation on the Ethereum network, the gas costs of execution will always be higher than private execution offchain. This incentivizes dapp developers to restrict the amount of code they execute and amount of data they store on the blockchain.

## Dapp directories <a id="dapp-directories"></a>

Dapps that use Ethereum are compiled to the following lists. They are listed in various stages of development \(concept, working prototype, live/deployed\). If you are developing a dapp, consider adding an entry to these listings:

* 
The offered decentralised services listed cover a wide range of areas including finance, insurance, prediction markets, social networks, distributed computation and storage, gambling, marketplace, internet of things, governance, collaboration, development and games.

* 
In the future, dapps are likely to be listed and distributed in dappstores integrated in dapp browsers.

## Dapp browsers <a id="dapp-browsers"></a>

* ​[Mist](https://github.com/ethereum/mist) - official GUI dapp browser developed by the foundation, alpha stage. Mist as Wallet dapp is in beta.
* ​[Status](https://status.im/) - Mobile Ethereum browser \(alpha\)
* ​[MetaMask](https://metamask.io/) - Aaron Kumavis Davis’s in-browser GUI. [Epicenter Bitcoin interview on github](https://www.reddit.com/r/ethereum/comments/3x97rg/aaron_davis_explains_the_differences_between/) - supported by DEVgrants
* ​[AlethZero](https://github.com/ethereum/alethzero) - C++ eth client GUI, \(discontinued\).
* ​[Supernova](http://www.supernove.cc/) - \(discontinued\).

Dapp development requires an understanding of the Web3 Javascript API, the JSON RPC API, and the Solidity programming language.

Note

There are developer tools that help you develop, test, and deploy dapps in a way that automatically utilizes the resources listed below.

* ​[Web3 JavaScript API](https://github.com/ethereum/wiki/wiki/JavaScript-API) - This is the main JavaScript SDK to use when you want to interact with an Ethereum node.
* ​[JSON RPC API](https://github.com/ethereum/wiki/wiki/JSON-RPC) - This is the low level JSON RPC 2.0 interface to interface with a node. This API is used by the [Web3 JavaScript API](https://github.com/ethereum/wiki/wiki/JavaScript-API).
* ​[Solidity Docs](https://solidity.readthedocs.org/en/latest/) - Solidity is the Ethereum developed Smart Contract language, which compiles to EVM \(Ethereum Virtual Machine\) opcodes.
* ​[Solium](https://github.com/duaraghav8/Solium/) - A linter for Solidity which strictly follows the rules prescribed by the official [Solidity Style Guide](http://solidity.readthedocs.io/en/latest/style-guide.html).
* ​[Test Networks](https://ethdocs.org/en/latest/network/test-networks.html#test-networks) - Test networks help developers develop and test Ethereum code and network interactions without spending their own ether on the main network. Test network options are listed below.
* ​[Dapp development resources](https://ethdocs.org/en/latest/contracts-and-transactions/developer-tools.html#ide-or-development-framework). This assists you in developing, debugging, and deploying Ethereum applications.

## Dapp development resources <a id="dapp-development-resources"></a>

* * * * 
### Examples <a id="examples"></a>

* * 
​[https://dappsforbeginners.wordpress.com/tutorials/your-first-dapp/](https://dappsforbeginners.wordpress.com/tutorials/your-first-dapp/)​

​[https://github.com/ethereum/wiki/wiki/Dapp-Developer-Resources](https://github.com/ethereum/wiki/wiki/Dapp-Developer-Resources)​

### Tutorials <a id="tutorials"></a>

* * * * * * 
## Mix-IDE <a id="mix-ide"></a>

Mix is the official Ethereum IDE that allows developers to build and deploy contracts and decentralized applications on top of the Ethereum blockchain. It includes a Solidity source code debugger. [Mix](https://ethdocs.org/en/latest/contracts-and-transactions/mix.html#sec-mix) \(discontinued\)

## IDEs/Frameworks <a id="ides-frameworks"></a>

Below are developer frameworks and IDEs used for writing Ethereum dapps.

* ​[Truffle](https://github.com/ConsenSys/truffle) - Truffle is a development environment, testing framework and asset pipeline for Ethereum.
* ​[Dapple](https://github.com/nexusdev/dapple) - Dapple is a tool for Solidity developers to help build and manage complex contract systems on Ethereum-like blockchains.
* ​[Populus](http://populus.readthedocs.org/en/latest/) - Populus is a Smart Contract development framework written in python.
* ​[Eris-PM](https://docs.erisindustries.com/documentation/eris-package-manager/) - The Eris Package Manager deploys and tests smart contract systems on private and public chains.
* ​[Embark](https://iurimatias.github.io/embark-framework/) - Embark is a Ðapp development framework written in JavaScript.
* * 
## Ethereum-console <a id="ethereum-console"></a>

Command-line console for Ethereum nodes.

​[Ethconsole](https://github.com/ethereum/ethereum-console) connects to an Ethereum node running in the background \(tested with eth and geth\) via IPC and provides an interactive javascript console containing the web3 object with admin additions.

Here you could find a list of available commands [ethereum node control commands](https://github.com/ethereum/ethereum-console/blob/master/web3Admin.js)​

To use this console you would need to start a local ethereum node with ipc communication socket enabled \(file `geth.ipc` in data directory\). By default ipc socket should be located at you local home directory in .ethereum after you started a node. You could also set `--test` option to use specific node test commands.

In the console you could then type

Here the defenition of `--test` mode node commands:

More information about node [configuration](https://ethdocs.org/en/latest/network/test-networks.html#custom-networks-eth) file.

## Base layer services <a id="base-layer-services"></a>

### Whisper <a id="whisper"></a>

* * ​[Gavin Wood: Shh! Whisper](https://www.youtube.com/watch?v=U_nPoBVLPiw) - DEVCON-1 talk youtube video
* * 
### Swarm <a id="swarm"></a>

Swarm is a distributed storage platform and content distribution service, a native base layer service of the Ethereum web 3 stack. The primary objective of Swarm is to provide a sufficiently decentralized and redundant store of Ethereum’s public record, in particular to store and distribute dapp code and data as well as block chain data. From an economic point of view, it allows participants to efficiently pool their storage and bandwidth resources in order to provide the aforementioned services to all participants.

From the end user’s perspective, Swarm is not that different from WWW, except that uploads are not to a specific server. The objective is to peer-to-peer storage and serving solution that is DDOS-resistant, zero-downtime, fault-tolerant and censorship-resistant as well as self-sustaining due to a built-in incentive system which uses peer to peer accounting and allows trading resources for payment. Swarm is designed to deeply integrate with the devp2p multiprotocol network layer of Ethereum as well as with the Ethereum blockchain for domain name resolution, service payments and content availability insurance.

**ÐΞVcon talks on swarm**

* ​[Viktor Trón, Daniel A. Nagy: Swarm](https://www.youtube.com/watch?v=VOC45AgZG5Q) - Ethereum ÐΞVcon-1 talk on youtube
* 
**Code and status**

* * * \[development roadmap\]\(\)
* * * 
Storage on and offchain

* * * 
### Ethereum Alarm Clock <a id="ethereum-alarm-clock"></a>

* **Author:** Piper Merriam
* * 
A marketplace that facilitates scheduling transactions to occur at a later time. Serves a similar role to things like _crontab_ in unix, or _setTimeout_ in javascript.

* 
### Ethereum Computation Market <a id="ethereum-computation-market"></a>

* **Author:** Piper Merriam
* * 
A marketplace that facilitates verifiable execution of computations off-chain. Allows for very expernsive computations to be used within the EVM without having to actually pay the high gas costs of executing them on-chain.

### BTCRelay <a id="btcrelay"></a>

​[BTCrelay](http://btcrelay.org/)​

* ​[More information](https://medium.com/@ConsenSys/taking-stock-bitcoin-and-ethereum-4382f0a2f17) \(about ETH/BTC 2-way peg without modifying bitcoin code\).
* 
### RANDAO <a id="randao"></a>

Random number \* [https://www.reddit.com/r/ethereum/comments/49yld7/eli5\_how\_does\_a\_service\_like\_szabodice\_grab\_a/](https://www.reddit.com/r/ethereum/comments/49yld7/eli5_how_does_a_service_like_szabodice_grab_a/)​

## The EVM <a id="the-evm"></a>

The Ethereum Virtual Machine \(EVM\) is the runtime environment for smart contracts in Ethereum. It is not only sandboxed, but actually completely isolated, which means that code running inside the EVM has no access to network, filesystem, or other processes. Smart contracts even have limited access to other smart contracts.

Contracts live on the blockchain in an Ethereum-specific binary format \(EVM bytecode\). However, contracts are typically written in an Ethereum high level language, compiled into byte code using an EVM compiler, and finally uploaded on the blockchain using an Ethereum client.

