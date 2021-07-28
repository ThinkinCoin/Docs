# List Instructions

Listing a trading pair is a rather advanced feature in DEX. To list your token, you can follow the step-by-step instruction here.

There are the steps to get your tokens listed:

![](https://docs.binance.org/assets/listing-workflow.jpg)

workflow

## Issue Tokens on Binance Chain <a id="issue-tokens-on-binance-chain"></a>

Please refer to this [token issue doc](https://docs.binance.org/tokens.html) to learn about how to issue your own asset on Binance Chain.

### Submit Proposal <a id="2-submit-proposal"></a>

_On-Chain Proposal Request_

Please refer to this [governance doc](https://docs.binance.org/governance.html) to learn about how to create a proposal about listing a new trading pair on Binance Chain.

> Please ensure that you test EVERYTHING on our testnet \(multiple times at least\) before you officially execute this on the mainnet.

_Community Thread Proposal \(Recommended\)_

It is recommended that Token Issuers first create a thread under the “Token Issuance & Listings” category in the Binance Chain Community Forum \([https://community.binance.org/\](https://community.binance.org//)\). The whole guideline is [here](https://community.binance.org/topic/18/guidelines-on-how-to-list-your-token-on-binance-dex)​

### Send List Transaction <a id="3-send-list-transaction"></a>

Please refer to this [list doc](https://docs.binance.org/list.html) to learn about how to send a list transaction and finish listing process on Binance Chain.

> Please ensure that a `list` transaction must be sent before `expire-time`.

## FAQ about Listing Tokens <a id="faq-about-listing-tokens"></a>

### Which trading pair can be listed? <a id="which-trading-pair-can-be-listed"></a>

Simply allowing trading between two assets seems easy enough, however it is expensive for not only the network but also its users in long term \(and liquidity costs can be much larger\). In order to efficiently use the network, Binance Chain only list assets against BNB and other widely accepted market quote assets.

### How is a trading pair created on Binance DEX? <a id="how-is-a-trading-pair-created-on-binance-dex"></a>

The design philosophy of Binance DEX adheres to the idea that the most efficient and low cost way to perform trading and price-discovery is still to use single order book. This single order book is managed and replicated across all full nodes with the same, deterministic matching logic.

