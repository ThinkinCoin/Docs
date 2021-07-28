# BSC Relayer

Relayers are responsible to submit Cross-Chain Communication Packages between the two blockchains. Due to the heterogeneous parallel chain structure, two different types of Relayers are created.

Relayers for BC-to-BSC communication referred to as **BSC Relayers** are a standalone process that can be run by anyone, and anywhere, except that Relayers must register themselves onto BSC and deposit a certain amount of BNB. Only relaying requests from the registered Relayers will be accepted by BSC.

GitHub Implementation link: [https://github.com/binance-chain/bsc-relayer](https://github.com/binance-chain/bsc-relayer)​

Config Files: [https://github.com/binance-chain/bsc-relayer-config](https://github.com/binance-chain/bsc-relayer-config)​

## Monitor and Parse Cross Chain Event <a id="monitor-and-parse-cross-chain-event"></a>

As a BSC relayer, it must have proper configurations on the following three items:

A BSC relayer is required to parse all block results and pick out all events with event type “IBCPackage” from endBlock event table. This is an cross chain package event example:

```text
{  "type": "IBCPackage",  "attributes":  [    {      "key": "IBCPackageInfo",      "value": "96::8::19"    }  ]}
```

BSC relayer should iterate all the attributes and parse the attribute value:

1. Split the value with “::” and get a 4-length string array
2. Follow the following table to parse the 4 elements:
3. Filter out attributes with mismatched destination chain CrossChainID.

## Build Tendermint Header and Query Cross Chain Package <a id="build-tendermint-header-and-query-cross-chain-package"></a>

```text
import tmtypes "github.com/tendermint/tendermint/types"type Header struct {  tmtypes.SignedHeader  ValidatorSet     *tmtypes.ValidatorSet `json:"validator_set"`  NextValidatorSet *tmtypes.ValidatorSet `json:"next_validator_set"`}
```

If a cross chain package event is found at height **H**, wait for block **H+1** and call the following rpc methods to build the above **Header** object:

Header Encoding in golang:

1. Add dependency on [go-amino v0.14.1](https://github.com/tendermint/go-amino/tree/v0.14.1)​
2. Add dependency on [tendermint v0.32.3](https://github.com/tendermint/tendermint/tree/v0.32.3):
3. Example golang code to encode **Header**:

   ```text
   import (  amino "github.com/tendermint/go-amino"  tmtypes "github.com/tendermint/tendermint/types")​var cdc = amino.NewCodec()​func init() {  tmtypes.RegisterBlockAmino(cdc)}​func EncodeHeader(h *Header) ([]byte, error) {  bz, err := cdc.MarshalBinaryLengthPrefixed(h)  if err != nil {     return nil, err  }  return bz, nil}
   ```

### Query Cross Chain Package With Merkle Proof <a id="query-cross-chain-package-with-merkle-proof"></a>

1. Query height: **H**
2. Query path: **/store/ibc/key**
3. Follow the table to build a 14-length byte array as query key:
4. Assemble the above parameters to the following rpc call.

   ```text
   {rpcEndpoint}/abci_query?path={queryPath}&data={queryKey}&height={queryHeight}&prove=true
   ```

## Call Build-In System Contract <a id="call-build-in-system-contract"></a>

* function **syncTendermintHeader**\(bytes calldata header, uint64 height\)

  Call **syncTendermintHeader** of TendermintLightClient contract to sync BC header. The contract address is 0x0000000000000000000000000000000000001003. The “header” is the encoding result of **Header** and the height should be **H+1**

### Deliver Cross Chain Package <a id="deliver-cross-chain-package"></a>

Call **handlePackage** of crosschain contract\(0x0000000000000000000000000000000000002000\) to deliver the cross chain packages:

## Incentives Mechanism <a id="incentives-mechanism"></a>

​[BSC Relayer Incentive Mechanism](https://docs.binance.org/smart-chain/guides/concepts/incentives.html)​

