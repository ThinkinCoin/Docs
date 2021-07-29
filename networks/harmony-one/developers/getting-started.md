# Getting Started

Harmony is a powerful blockchain that is EVM compatible with sharding and [staking](https://docs.harmony.one/home/validators) features. Developing on Harmony should feel very familiar for Ethereum developers, as Harmony is [fully Ethereum compatible](https://medium.com/harmony-one/launching-full-ethereum-compatibility-on-harmony-e181ed3c6a24) and inherits almost all the tools and libraries from Ethereum, like truffle, remix, web3js, etc.

The simplest way to interact with Harmony blockchain is via JSON RPCs.

### Querying Harmony blockchian using JSON RPCs <a id="querying-harmony-blockchian-using-json-rpcs"></a>

* JSON [RPCs](api.md) and `curl` command [examples](https://docs.harmony.one/home/developers/api/methods)​

To really explore the full potential of Harmony blockchain, creating a wallet is the next step.

### Creating a wallet \(or ONE address\) <a id="creating-a-wallet-or-one-address"></a>

* Using [onewallet](https://docs.harmony.one/home/wallets/browser-extensions-wallets/one-wallet) or [mathwallet](https://docs.harmony.one/home/wallets/browser-extensions-wallets/mathwallet) browser extensions. Any other [wallets](https://docs.harmony.one/home/wallets) can also be used.
* Harmony [CLI](https://docs.harmony.one/home/wallets/harmony-cli), also provides a quick way to create/manage wallet, interact with blockchain, etc.

Harmony uses [bech32](https://en.bitcoin.it/wiki/Bech32) address format with `one1` prefix, however Ethereum style hex address can also be used. For example: `one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy` bech32 address is equivalent to `0x0B585F8DaEfBC68a311FbD4cB20d9174aD174016` hex address. Quick way to convert between formats is using explorer: [https://explorer.harmony.one/\#/address/one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy](https://explorer.harmony.one/#/address/one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy), at the top you will find "Address Format" ONE \| ETH options.

### Development environments <a id="development-environments"></a>

* Several development environments exists: [mainnet, testnnet, localnet](https://docs.harmony.one/home/developers/api#development-environments)​
* * We provide SDKs in several different languages. However most feature complete is our JavaScript SDK, which is the preferred language for DApp development.

### Using SDKs to interact with Harmony blockchian <a id="using-sdks-to-interact-with-harmony-blockchian"></a>

* * The most popular is our [JavaScript SDK](https://github.com/harmony-one/sdk), which includes examples, documentation, and DApps developed in previous hackathons
* Other SDKs include: Golang CLI, Java SDK, Python SDK
  * Note that, the Python SDK has only read-only features, meaning no transaction signing or smart contracts

## How to deploy a smart contract on Harmony? <a id="how-to-deploy-a-smart-contract-on-harmony"></a>

## How to create a simple DApp on Harmony? <a id="how-to-create-a-simple-dapp-on-harmony"></a>

* * Many other examples and DApps can be found in the [SDK repo](https://github.com/harmony-one/sdk) and under [showcases](https://docs.harmony.one/home/showcases).

## Resources <a id="resources"></a>

* ​[talk.harmony.one](https://talk.harmony.one/c/developers/31) - for reporting issues, asking questions, or interact with other developers

## Known Limitations <a id="known-limitations"></a>

* **Only cross-shard native token \(ONE token\) transfers** are allowed. No cross-shard for HRC20 or other contracts. Meaning, smart contracts are deployed on shard-0 and all contract interactions happen on shard-0. Contracts can still be deployed on other shards, however they won't be able to interact with contracts in other shards. We have cross-shard smart contract on our roadmap for Q3, 2021.

