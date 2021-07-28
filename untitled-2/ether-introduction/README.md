# Ether - Introduction

## What is ether? <a id="what-is-ether"></a>

Ether is the name of the currency used within Ethereum. It is used to pay for computation within the EVM. This is done indirectly by purchasing gas for ether as explained in gas.

### Denominations <a id="denominations"></a>

Ethereum has a metric system of denominations used as units of ether. Each denomination has its own unique name \(some bear the family name of seminal figures playing a role in evolution of computer science and cryptoeconomics\). The smallest denomination aka _base unit_ of ether is called Wei. Below is a list of the named denominations and their value in Wei. Following a common \(although somewhat ambiguous\) pattern, ether also designates a unit \(of 1e18 or one quintillion Wei\) of the currency. Note that the currency is not called Ethereum as many mistakenly think, nor is Ethereum a unit.

## Getting ether <a id="getting-ether"></a>

In order to obtain Ether, you need to either

* become an Ethereum miner \(see Mining\) or
* trade other currencies for ether using centralised or trustless services
* use the user friendly [Mist Ethereum GUI Wallet](https://github.com/ethereum/mist/releases) that as of Beta 6 introduced the ability to purchase ether using the [http://shapeshift.io/](http://shapeshift.io/) API.

### Trustless services <a id="trustless-services"></a>

Note that the Ethereum platform is special in that the smart contracts enable trustless services that obviate the need for trusted third parties in a currency exchange transaction, ie. disintermediate currency exchange businesses.

Such projects \(alpha/prelaunch status at the time of writing\) are:

* ​[BTCrelay](http://btcrelay.org/)​
  * ​[More information](https://medium.com/@ConsenSys/taking-stock-bitcoin-and-ethereum-4382f0a2f17) \(about ETH/BTC 2-way peg without modifying bitcoin code\).
  * 
* 
### List of centralised exchange marketplaces <a id="list-of-centralised-exchange-marketplaces"></a>

### Centralised fixed rate exchanges <a id="centralised-fixed-rate-exchanges"></a>

## Sending ether <a id="sending-ether"></a>

The [Ethereum Wallet](https://github.com/ethereum/mist/releases) supports sending ether via a graphical interface.

Ether can also be transferred using the **geth console**.

```text
> var sender = eth.accounts[0];> var receiver = eth.accounts[1];> var amount = web3.toWei(0.01, "ether")> eth.sendTransaction({from:sender, to:receiver, value: amount})
```

For more information of ether transfer transactions, see [Account Types, Gas, and Transactions](https://ethdocs.org/en/latest/contracts-and-transactions/account-types-gas-and-transactions.html#account-types-gas-and-transactions).

Ethereum is unique in the realm of cryptocurrencies in that ether has utility value as a cryptofuel, commonly referred to as “gas”. Beyond transaction fees, gas is a central part of every network request and requires the sender to pay for the computing resources consumed. The gas cost is dynamically calculated, based on the volume and complexity of the request and multiplied by the current gas price. Its value as a cryptofuel has the effect of increasing the stability and long-term demand for ether and Ethereum as a whole. For more information, see [Account Types, Gas, and Transactions](https://ethdocs.org/en/latest/contracts-and-transactions/account-types-gas-and-transactions.html#account-types-gas-and-transactions).

## Gas and ether <a id="gas-and-ether"></a>

* * * 
Gas is supposed to be the constant cost of network resources/utilisation. You want the real cost of sending a transaction to always be the same, so you can’t really expect Gas to be issued, currencies in general are volatile.

So instead, we issue ether whose value is supposed to vary, but also implement a Gas Price in terms of Ether. If the price of ether goes up, the Gas Price in terms of ether should go down to keep the real cost of Gas the same.

Gas has multiple associated terms with it: Gas Prices, Gas Cost, Gas Limit, and Gas Fees. The principle behind Gas is to have a stable value for how much a transaction or computation costs on the Ethereum network.

* Gas Cost is a static value for how much a computation costs in terms of Gas, and the intent is that the real value of the Gas never changes, so this cost should always stay stable over time.
* Gas Price is how much Gas costs in terms of another currency or token like Ether. To stabilise the value of gas, the Gas Price is a floating value such that if the cost of tokens or currency fluctuates, the Gas Price changes to keep the same real value. The Gas Price is set by the equilibrium price of how much users are willing to spend, and how much processing nodes are willing to accept.
* Gas Limit is the maximum amount of Gas that can be used per block, it is considered the maximum computational load, transaction volume, or block size of a block, and miners can slowly change this value over time.
* Gas Fee is effectively the amount of Gas needed to be paid to run a particular transaction or program \(called a contract\). The Gas Fees of a block can be used to imply the computational load, transaction volume, or size of a block. The gas fees are paid to the miners \(or bonded contractors in PoS\).

