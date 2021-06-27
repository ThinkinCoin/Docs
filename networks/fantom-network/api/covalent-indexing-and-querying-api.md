# Covalent indexing and querying API

## Supported endpoints <a id="supported-endpoints"></a>

All Covalent **Class A** endpoints are supported for the Fantom mainnet and testnet. You can query the network via the unified API by changing the`chainId`parameter:

* Mainnet: `250`
* Testnet: `4002`

All requests to the Covalent API are done over HTTPS \(calls over plain HTTP will fail.\)

* `api.covalenthq.com/v1/{chainId}/address/{address}/balances_v2/`
  * Get token balances for `address`. Return a list of all ERC20 and NFT token balances including ERC721 and ERC1155 along with their current spot prices.
* `api.covalenthq.com/v1/{chainId}/address/{address}/transactions_v2/`
  * Retrieve all transactions for `address` including their decoded log events. This endpoint does a deep-crawl of the blockchain to retrieve all kinds of transactions that references the address.
* `api.covalenthq.com/v1/{chainId}/address/{address}/transfers_v2/`
  * Get ERC20 token transfers for `address` along with historical token prices.
* `api.covalenthq.com/v1/{chainId}/tokens/{contract_address}/token_holders/`
  * Return a paginated list of token holders `contract_address` as of any historical block height.
* `api.covalenthq.com/v1/{chainId}/events/address/{contract_address}/`
  * Return a paginated list of decoded log events emitted by a particular smart contract.
* `api.covalenthq.com/v1/{chainId}/events/topics/{topic}/`
  * Return a paginated list of decoded log events with one or more topic hashes separated by a comma.

​[Go to Covalent's API Reference](https://www.covalenthq.com/docs/api/)​

## ​[​](https://www.covalenthq.com/docs/networks/fantom#appendix)Appendix <a id="appendix"></a>

### ​[​](https://www.covalenthq.com/docs/networks/fantom#fantom-token)Fantom token <a id="fantom-token"></a>

The Fantom token `FTM` is the native token of Fantom. This is similar to Ether in Ethereum. To interact with the Fantom network, FTM tokens are required to pay gas fees. The Covalent API response returns `gas_*` fields in fiat units.

### ​[​](https://www.covalenthq.com/docs/networks/fantom#token-mapping)Token mapping <a id="token-mapping"></a>

Covalent maintains an on-chain real-time mapping of token addresses between Ethereum mainnet and the Fantom chain. These addresses are used to reverse-lookup prices on Fantom and also to return the right token logo urls.

Some example of mapped tokens:

For the current token mapping list, see: [https://netapi.anyswap.net/bridge/v2/info](https://netapi.anyswap.net/bridge/v2/info)​

### ​[​](https://www.covalenthq.com/docs/networks/fantom#token-prices)Token prices <a id="token-prices"></a>

For tokens that have a mapping back to Ethereum mainnet, Covalent is able to return the mapped prices.

