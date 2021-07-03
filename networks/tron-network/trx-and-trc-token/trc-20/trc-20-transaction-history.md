# TRC-20 transaction history

## Get TRC-20 transaction history

**Get the transaction history for a specific TRC-20 in a specific account.**

API documents references

* [Get Transaction history](https://developers.tron.network/docs/get-history)
* [Get TRC-20 transaction info by account address](https://developers.tron.network/reference-link/trc20-transaction-information-by-account-address)

Shell

```text
curl --request GET \
  --url 'https://api.trongrid.io/v1/accounts/TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh/transactions/trc20?limit=100&contract_address=TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t'

Parameters：
version:The latest version v1.
address: account address，in Base58 or Hex.
only_confirmed:  true|false. if false, returns both confirmed & unconfirmed transactions; if no parameters, returns both confirmed & unconfirmed transactions. CAN NOT be used with only_unconfirmed.
only_unconfirmed: true|false. if false，returns both confirmed & unconfirmed transactions; if no parameters, returns both confirmed & unconfirmed transactions. CAN NOT be used with only_confirmed.
limit:transactions per page，default is 20, maximum is 200.
fingerprint：The fingerprint of the last transaction returned on the previous page
. When using this, other parameters and filters should remain unchanged.
contract_address：TRC20 contract address, Base58 or Hex.

//Example
//Get transactions related to TRC20 USDT on the address TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh
curl --request GET \
  --url ' https://api.trongrid.io/v1/accounts/TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh/transactions/trc20?limit=20&contract_address=TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t'
```

