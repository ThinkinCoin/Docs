# API

**Complete documentation for Harmony's API's production API's can be found** [**here**](https://api.hmny.io/?version=latest) **including sample code and curl commands and code.**

## Development Environments <a id="development-environments"></a>

​[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data from the Harmony nodes. The JSON-RPC API server runs on:

Web sockets can also be used

All requests follow the standard JSON-RPC format and include 4 variables in the data object:

### Key Differences between Harmony and Ethereum <a id="key-differences-between-harmony-and-ethereum"></a>

1. The prefix of RPC calls is different - **'hmy' for API v1** or **'hmyv2' for API v2** is used instead of 'eth'. Note that, Harmony also fully supports most `eth_` rpcs defined in [here](https://eth.wiki/json-rpc/API).
2. Address format: Harmony uses [bech32](https://en.bitcoin.it/wiki/Bech32) address format with `one1` prefix, however Ethereum style hex address can also be used. For example: `one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy` bech32 address is equivalent to `0x0B585F8DaEfBC68a311FbD4cB20d9174aD174016` hex address. Quick way to convert between formats is using explorer: [https://explorer.harmony.one/\#/address/one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy](https://explorer.harmony.one/#/address/one1pdv9lrdwl0rg5vglh4xtyrv3wjk3wsqket7zxy), at the top you will find "Address Format" ONE \| ETH options.
3. Harmony transactions are encoded using RLP, with two additional fields to represent from and to shard ids \(`shardID` and `toShardID`\), which is where it differs from Ethereum v1.

### API v1 and v2 <a id="api-v1-and-v2"></a>

1. **Harmony API has two versions**: **v1 with prefix 'hmy',** which returns hex numbers in API json response and **v2 with prefix 'hmyv2'** which mostly returns decimal numbers in API json response.
2. For each method which curl and response are different for API v1 and API v2: **there are two sections in description for API v1 and API v2** with examples. If there are no sections then examples are the same for v1 and v2 and can be quired both with 'hmy' prefix and 'hmyv2' prefix same way.
3. You can see in API response examples which variables **correspond to 0x format** and which to **decimal format**

