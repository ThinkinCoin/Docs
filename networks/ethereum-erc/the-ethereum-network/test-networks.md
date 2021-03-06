# Test Networks

## eth \(C++ client\)

It is possible to connect to or create a new network by using the –genesis and –config.

It is possible to use both –config and –genesis.

In that case, the genesis block description provided by –config will be overwritten by the –genesis option.

Note

 contains a JSON description of the network:

* sealEngine \(engine use to mine block\)

  > “Ethash” is the Ethereum proof of work engine \(used by the live network\).
  >
  > “NoProof” no proof of work is needed to mine a block.

* params \(general network information like minGasLimit, minimumDifficulty, blockReward, networkID\)
* genesis \(genesis block description\)
* accounts \(setup an original state that contains accounts/contracts\)

Here is a Config sample \(used by the Olympic network\):

Note

 contains a JSON description of the genesis block:

The content is the same as the genesis field provided by the ‘config’ parameter:

## geth \(Go client\)

You either pre-generate or mine your own ether on a private testnet. It is a much more cost effective way of trying out Ethereum and you can avoid having to mine or find Morden test ether.The things that are required to specify in a private chain are:

* Custom Genesis File
* Custom Data Directory
* Custom NetworkID
* \(Recommended\) Disable Node Discovery

### The genesis file

The genesis block is the start of the blockchain - the first block, block 0, and the only block that does not point to a predecessor block. The protocol ensures that no other node will agree with your version of the blockchain unless they have the same genesis block, so you can make as many private testnet blockchains as you’d like!

`CustomGenesis.json`

```text
{
    "nonce": "0x0000000000000042",     "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x0",     "gasLimit": "0x8000000",     "difficulty": "0x400",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",     "alloc": {     }
}
```

Save a file called `CustomGenesis.json`. You will reference this when starting your geth node using the following command:

`geth init /path/to/CustomGenesis.json`

Note

By default geth will use the same directory for network related files as for the public mainnet. Thus you are advised to set a custom `--datadir` to keep the public network’s chaindata from bing reset.

### Command line parameters for private network

There are some command line options \(also called “flags”\) that are necessary in order to make sure that your network is private. We already covered the genesis flag, but we need a few more. Note that all of the commands below are to be used in the geth Ethereum client.

`--nodiscover`

Use this to make sure that your node is not discoverable by people who do not manually add you. Otherwise, there is a chance that your node may be inadvertently added to a stranger’s blockchain if they have the same genesis file and network id.

`--maxpeers 0`

Use maxpeers 0 if you do not want anyone else connecting to your test chain. Alternatively, you can adjust this number if you know exactly how many peers you want connecting to your node.

`--rpc`

This will enable RPC interface on your node. This is generally enabled by default in Geth.

`--rpcapi "db,eth,net,web3"`

This dictates what APIs that are allowed to be accessed over RPC. By default, Geth enables the web3 interface over RPC.

**IMPORTANT: Please note that offering an API over the RPC/IPC interface will give everyone access to the API who can access this interface \(e.g. dapp’s\). Be careful which API’s you enable. By default geth enables all API’s over the IPC interface and only the db,eth,net and web3 API’s over the RPC interface.**

`--rpcport "8080"`

Change 8000 to any port that is open on your network. The default for geth is 8080.

`--rpccorsdomain "http://chriseth.github.io/browser-solidity/"`

This dictates what URLs can connect to your node in order to perform RPC client tasks. Be very careful with this and type a specific URL rather than the wildcard \(\*\) which would allow any URL to connect to your RPC instance.

`--datadir "/home/TestChain1"`

This is the data directory that your private chain data will be stored in \(under the `nubits` . Choose a location that is separate from your public Ethereum chain folder.

`--port "30303"`

This is the “network listening port”, which you will use to connect with other peers manually.

`--identity "TestnetMainNode"`

This will set up an identity for your node so it can be identified more easily in a list of peers. Here is an example of how these identities show up on the network.

### Launching `geth`

After you have created your custom genesis block JSON file and created a directory for your blockchain data, type the following command into your console that has access to geth:

```text
geth --identity "MyNodeName" --rpc --rpcport "8080" --rpccorsdomain "*" --datadir "C:\chains\TestChain1" --port "30303" --nodiscover --rpcapi "db,eth,net,web3" --networkid 1999 init /path/to/CustomGenesis.json
```

Note

Please change the flags to match your custom settings.

This will initialize your genesis block. To interact with geth through the console enter:

```text
geth --identity "MyNodeName" --rpc --rpcport "8080" --rpccorsdomain "*" --datadir "C:\chains\TestChain1" --port "30303" --nodiscover --rpcapi "db,eth,net,web3" --networkid 1999 console
```

You will need to start your geth instance with your custom chain command every time you want to access your custom chain. If you just type “geth” in your console, it will not remember all of the flags you have set.

The full list of methods available through the javascript console is available on [the geth wiki on github](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console)

If you already have a geth node running, you can attach another geth instance to it using:

Now you’ll need to initialize a new account on the testnest, and set it as your etherbase \(the address that will receive mining rewards\).

In the javascript console type

```text
personal.newAccount("password")
```

Note

Replace with the password of your choice

Now we’ll set it as the etherbase:

```text
miner.setEtherbase(personal.listAccounts[0])
```

If successful, the console will print “true”

Finally, you are ready to start mining test ether:

### Pre-allocating ether to your account

A difficulty of “0x400” allows you to mine Ether very quickly on your private testnet chain. If you create your chain and start mining, you should have hundreds of ether in a matter of minutes which is way more than enough to test transactions on your network. If you would still like to pre-allocate Ether to your account, you will need to:

1. Create a new Ethereum account after you create your private chain
2. Copy your new account address
3. Add the following command to your Custom\_Genesis.json file:

```text
"alloc":
{
        "":
        { "balance": "20000000000000000000" }
}
```

Note

Replace `0x1fb891f92eb557f4d688463d0d7c560552263b5a` with your account address.

Save your genesis file and rerun your private chain command. Once geth is fully loaded, close it by .

We want to assign an address to the variable `primary` and check its balance.

Run the command `geth account list` in your terminal to see what account \# your new address was assigned.

```text
> geth account list
Account #0: {d1ade25ccd3d550a7eb532ac759cac7be09c2719}
Account #1: {da65665fc30803cb1fb7e6d86691e20b1826dee0}
Account #2: {e470b1a7d2c9c5c6f03bbaa8fa20db6d404a0c32}
Account #3: {f4dd5c3794f1fd0cdc0327a83aa472609c806e99}
```

Take note of which account \# is the one that you pre-allocated ether to. Alternatively, you can launch the console with `geth console` \(keep the same parameters as when you launched `geth` first\). Once the prompt appears, type

This will return the array of account addresses you possess.

```text
> primary = eth.accounts[0]
```

Note

Replace `0` with your account’s index. This console command should return your primary Ethereum address.

Type the following command:

```text
> balance = web3.fromWei(eth.getBalance(primary), "ether");
```

This should return `7.5` indicating you have that much ether in your account. The reason we had to put such a large number in the alloc section of your genesis file is because the “balance” field takes a number in wei which is the smallest denomination of the Ethereum currency ether \(see Ether\).

* [https://www.reddit.com/r/ethereum/comments/3kdnus/question\_about\_private\_chain\_mining\_dont\_upvote/](https://www.reddit.com/r/ethereum/comments/3kdnus/question_about_private_chain_mining_dont_upvote/)

