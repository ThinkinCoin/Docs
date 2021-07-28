# Fees

**BNB** is the native token on Binance Chain, thus users are charged BNB for sending transactions.

### Trading Fees on DEX <a id="trading-fees-on-dex"></a>

Trading fees are subject to complex logic that may mean that individual trades are not charged exactly by the rates below, but between them instead; this is due to the block-based matching engine in use on the DEX.

The current fee for trades, applied on the settled amounts, is as follows:

Trading fee can be queried at [here](https://dex.binance.org/api/v1/fees?format=amino). It's under the "params/DexFeeParam/". "FeeRate" and "FeeRateNative" are both under unit of 10^-6.

### Fix Fee Table <a id="fix-fee-table"></a>

The difference between Binance Chain and Ethereum is that there is no notion of `gas`. As a result, fees for the rest transactions are fixed. The details are showned in the table below:

* Current Fees Table on Mainnet
* Current Fees Table on Testnet

### How to calculate multisend fee <a id="how-to-calculate-multisend-fee"></a>

`bnbcli` offers you a multi-send command to transfer multiple tokens to multiple people. 20% discount is available for `multi-send` transactions. For now, `multi-send` transaction will send some tokens from one address to multiple output addresses. If the count of output address is bigger than the threshold, currently it's 2, then the total transaction fee is 0.001 BNB per token per address. For example, if you send 3 ABC token,1 SAT token and 1 ABC to 3 different addresses.

```text
[   {      "to":"bnb1g5p04snezgpky203fq6da9qyjsy2k9kzr5yuhl",      "amount":"100000000:BNB,100000000:ABC"   },   {      "to":"bnb1l86xty0m55ryct9pnypz6chvtsmpyewmhrqwxw",      "amount":"100000000:BNB"   },   {      "to":"bnb1l86xty0maxdgst9pnypz6chvtsmpydkjflfioe",      "amount":"100000000:BNB,100000000:SAT"   }]
```

You will pay on mainnet/testnet

```text
0.0003 BNB * 5 = 0.0015 BNB
```

## How are rewards distributed between validators? <a id="how-are-rewards-distributed-between-validators"></a>

you can use [API](https://dex.binance.org/api/v1/fees) to get the latest fee params.

```text
[{msg_type: "submit_proposal",fee: 500000000,fee_for: 1},{msg_type: "deposit",fee: 62500,fee_for: 1},{msg_type: "vote",fee: 0,fee_for: 3},{msg_type: "create_validator",fee: 1000000000,fee_for: 1},{msg_type: "remove_validator",fee: 100000000,fee_for: 1},{msg_type: "dexList",fee: 100000000000,fee_for: 2},{msg_type: "orderNew",fee: 0,fee_for: 3},{msg_type: "orderCancel",fee: 0,fee_for: 3},{msg_type: "issueMsg",fee: 50000000000,fee_for: 2},{msg_type: "mintMsg",fee: 500000000,fee_for: 2},{msg_type: "tokensBurn",fee: 50000000,fee_for: 1},{msg_type: "tokensFreeze",fee: 500000,fee_for: 1},{fixed_fee_params: {msg_type: "send",fee: 37500,fee_for: 1},multi_transfer_fee: 30000,lower_limit_as_multi: 2},{dex_fee_fields: [{fee_name: "ExpireFee",fee_value: 25000},{fee_name: "ExpireFeeNative",fee_value: 5000},{fee_name: "CancelFee",fee_value: 25000},{fee_name: "CancelFeeNative",fee_value: 5000},{fee_name: "FeeRate",fee_value: 1000},{fee_name: "FeeRateNative",fee_value: 400},{fee_name: "IOCExpireFee",fee_value: 10000},{fee_name: "IOCExpireFeeNative",fee_value: 2500}]},{msg_type: "timeLock",fee: 1000000,fee_for: 1},{msg_type: "timeUnlock",fee: 1000000,fee_for: 1},{msg_type: "timeRelock",fee: 1000000,fee_for: 1},{msg_type: "setAccountFlags",fee: 100000000,fee_for: 1},{msg_type: "HTLT",fee: 37500,fee_for: 1},{msg_type: "depositHTLT",fee: 37500,fee_for: 1},{msg_type: "claimHTLT",fee: 37500,fee_for: 1},{msg_type: "refundHTLT",fee: 37500,fee_for: 1}]
```

The `fee_for`parameter indicate the different distribution way:

* `1` means rewards is only for block proposer
* `2` means rewards are shared among all validators
* `3` means fee is free.

## How to query fees in every block <a id="how-to-query-fees-in-every-block"></a>

The rewards for Binance Chain validators are displayed in explorer. For example: in block [59947302](https://explorer.binance.org/block/59947302), validator [bnb1tpagqqqx36gq09kzw4f5a3a9sk3tq54dpl5ldn](https://explorer.binance.org/address/bnb1tpagqqqx36gq09kzw4f5a3a9sk3tq54dpl5ldn) get `0.00005 BNB` as rewards.

If you have a fullnode running, you can also get the rewards details exported. To achieve this, you need to set `publishBlockFee` to be true in your `app.toml`. To receive rewards stream, there aretwo options `publishKafka` and `publishLocal`

```text
# Whether we want publish block fee changespublishBlockFee = trueblockFeeTopic = "accounts"blockFeeKafka = "127.0.0.1:9092"# Global settingpublicationChannelSize = "10000"publishKafka = falsepublishLocal = true
```

The rewards history are saved under `{fullnode home}/marketdata/marketdata.json`. For example,

> Note: Quantities here are expressed without decimals, i.e. shifted by 10^8

```text
{"Height":59947302,"Fee":"BNB:5000","Validators":["bnb1tpagqqqx36gq09kzw4f5a3a9sk3tq54dpl5ldn"]}{"Height":59947303,"Fee":"BNB:5000","Validators":["bnb1y888axmhzz6yjj464syfy68mkhzy9phlv8fzac"]}{"Height":59947304,"Fee":"BNB:5000","Validators":["bnb19klje94mnu53wj7pmrk0zmtpwgr0uz8th0fcvw"]}{"Height":59947305,"Fee":"BNB:21364","Validators":["bnb19hunw9ps8n9tkrp2j64jvheezgqmfc2eyrxd7a"]}{"Height":59947306,"Fee":"","Validators":[]}...{"Height":59947480,"Fee":"BUSD-BD1:1486828;XRP-BF2:3311258","Validators":["bnb19klje94mnu53wj7pmrk0zmtpwgr0uz8th0fcvw"]}...
```

Trading fees can be charged in different BEP2 tokens,

