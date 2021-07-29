# Swagger API reference

API description for swap service

**Version:** V1.0

**Contact information:** Binance Chain

**Base URL:** api.binance.org/bridge

**Rate Limit:** 2000 request per IP per 5 mins.

### /api/v1/tokens

**GET**

**Summary:** get

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| direction | query | IN or OUT | No | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 20000 | OK | TokenList |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v1/tokens/{symbol}/networks

**GET**

**Summary:** get

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| symbol | path | token symbol | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | NetworkList |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v1/swaps

**GET**

**Summary:** find swap

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| direction | query | direction | No | string |
| endTime | query | endTime | No | long |
| limit | query | limit | No | long |
| offset | query | offset | No | long |
| startTime | query | startTime | No | long |
| status | query | status | No | \[ string \] |
| symbol | query | symbol | No | string |
| walletAddress | query | walletAddress | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | ResponseStatusBodySwapList |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

**POST**

**Summary:** create

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| payload | body | payload | Yes | SwapCreationRequest |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | ResponseStatusBodySwapCreation |
| 201 | Created |  |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v1/swaps/{swapId}

**GET**

**Summary:** get

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| swapId | path | swapId | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | ResponseStatusBodySwapDetail |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v1/swaps/{swapId}/email

**PUT**

**Summary:** create Email

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| payload | body | payload | Yes | EmailUpdateRequest |
| swapId | path | swapId | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | ResponseStatus |
| 201 | Created |  |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v1/swaps/quota/24hour

**GET**

**Summary:** getQuota

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| symbol | query | symbol | Yes | string |
| walletAddress | query | walletAddress | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 200 | OK | ResponseStatusBodyQuota |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v2/swaps

**GET**

**Summary:** find swap V2

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| endTime | query | endTime | No | long |
| limit | query | limit | No | long |
| offset | query | offset | No | long |
| startTime | query | startTime | No | long |
| status | query | status | No | \[ string \] |
| symbol | query | symbol | No | string |
| walletAddress | query | walletAddress | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 20000 | OK | ResponseStatusBodySwapList |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

**POST**

**Summary:** createV2

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| payload | body | payload | Yes | SwapCreationRequestV2 |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 20000 | OK | ResponseStatusBodySwapCreation |
| 20001 | Created |  |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v2/tokens

**GET**

**Summary:** getQuota

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 20000 | OK | TokenListV2 |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

### /api/v2/tokens/{symbol}/networks

**GET**

**Summary:** get

**Parameters**

| Name | Located in | Description | Required | Schema |
| :--- | :--- | :--- | :--- | :--- |
| symbol | path | token symbol | Yes | string |

**Responses**

| Code | Description | Schema |
| :--- | :--- | :--- |
| 20000 | OK | NetworkListV2 |
| 401 | Unauthorized |  |
| 403 | Forbidden |  |
| 404 | Not Found |  |

## Models

### EmailUpdateRequest

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| email | string |  |  |
| walletAddress | string |  |  |

### ResponseStatus

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| code | integer |  |  |
| message | string |  |  |

### ResponseStatusBodySwapCreation

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| code | integer |  |  |
| data | SwapCreation |  |  |
| message | string |  |  |

### ResponseStatusBodySwapDetail

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| code | integer |  |  |
| data | SwapDetail |  |  |
| message | string |  |  |

### SwapCreation

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| amount | number |  |  |
| createTime | dateTime |  |  |
| depositAddress | string |  |  |
| depositAddressLabel | string |  |  |
| depositTimeout | dateTime |  |  |
| direction | string |  |  |
| fromNetwork | string |  |  |
| id | string |  |  |
| networkFee | number |  |  |
| networkFeePromoted | boolean |  |  |
| status | string |  |  |
| swapFee | number |  |  |
| swapFeeRate | number |  |  |
| symbol | string |  |  |
| toAddress | string |  |  |
| toAddressLabel | string |  |  |
| toNetwork | string |  |  |
| walletAddress | string |  |  |

### SwapCreationRequest

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| amount | number |  |  |
| direction | string |  |  |
| fromNetwork | string |  |  |
| source | integer |  |  |
| symbol | string |  |  |
| toAddress | string |  |  |
| toAddressLabel | string |  |  |
| toNetwork | string |  |  |
| walletAddress | string |  |  |

### SwapDetail

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| actualFromAmount | number |  |  |
| actualNetworkFee | number |  |  |
| actualSwapFee | number |  |  |
| actualToAmount | number |  |  |
| amount | number |  |  |
| createTime | dateTime |  |  |
| depositAddress | string |  |  |
| depositAddressLabel | string |  |  |
| depositReceivedConfirms | integer |  |  |
| depositRequiredConfirms | integer |  |  |
| depositTimeout | dateTime |  |  |
| depositTxId | string |  |  |
| depositTxLink | string |  |  |
| direction | string |  |  |
| fromNetwork | string |  |  |
| id | string |  |  |
| networkFee | number |  |  |
| networkFeePromoted | boolean |  |  |
| status | string |  |  |
| swapFee | number |  |  |
| swapFeeRate | number |  |  |
| swapTxId | string |  |  |
| swapTxLink | string |  |  |
| symbol | string |  |  |
| toAddress | string |  |  |
| toAddressLabel | string |  |  |
| toNetwork | string |  |  |
| updateTime | dateTime |  |  |
| walletAddress | string |  |  |

### ResponseStatusBodySwapList

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| code | integer |  |  |
| data | SwapList |  |  |
| message | string |  |  |

### SwapList

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| swaps | \[ SwapDetail \] |  |  |
| total | long |  |  |

### TokenList

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| swaps | \[ TokenDetail \] |  |  |
| total | long |  |  |

### TokenListV2

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| swaps | \[ TokenDetailV2 \] |  |  |
| total | long |  |  |

### TokenDetail

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| name | string |  |  |
| symbol | string |  |  |
| bcSymbol | string |  |  |
| icon | string |  |  |
| minAmount | number |  |  |
| maxAmount | number |  |  |
| promotion | boolean |  |  |
| enabled | boolean |  |  |
| bscContractAddress | string |  |  |
| bscContractDecimal | integer |  |  |

### TokenDetailV2

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| name | string |  |  |
| symbol | string |  |  |
| bcSymbol | string |  |  |
| ethSymbol | string |  |  |
| icon | string |  |  |
| minAmount | number |  |  |
| maxAmount | number |  |  |
| promotion | boolean |  |  |
| enabled | boolean |  |  |
| bscContractAddress | string |  |  |
| bscContractDecimal | integer |  |  |
| ethContractAddress | string |  |  |
| ethContractDecimal | integer |  |  |

### NetworkList

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| from | \[ NetworkDetail \] |  |  |
| to | \[ NetworkDetail \] |  |  |

### NetworkDetail

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| name | string |  |  |
| supportLabel | boolean |  |  |
| labelName | string |  |  |
| labelRegex | string |  |  |
| txUrl | number |  |  |
| enabled | boolean |  |  |
| requiredConfirms | integer |  |  |
| tokenStandard | string |  |  |

### NetworkListV2

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| from | \[ NetworkDetailV2 \] |  |  |
| to | \[ NetworkDetailV2 \] |  |  |

### NetworkDetailV2

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| name | string |  |  |
| symbol | string |  |  |
| swapFeeRate | number |  |  |
| networkFee | number |  |  |
| supportLabel | boolean |  |  |
| labelName | string |  |  |
| labelRegex | string |  |  |
| txUrl | number |  |  |
| depositEnabled | boolean |  |  |
| withdrawEnabled | boolean |  |  |
| withdrawAmountUnit | number |  |  |
| addressRegex | string |  |  |
| tokenStandard | string |  |  |
| requiredConfirms | integer |  |  |

### ResponseStatusBodyQuota

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| code | integer |  |  |
| data | Quota |  |  |
| message | string |  |  |

### Quota

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| left | number |  |  |
| total | number |  |  |
| used | number |  |  |

### SwapCreationRequestV2

| Name | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| amount | number |  |  |
| fromNetwork | string |  |  |
| source | integer |  |  |
| symbol | string |  |  |
| toAddress | string |  |  |
| toAddressLabel | string |  |  |
| toNetwork | string |  |  |
| walletAddress | string |  |  |
| walletNetwork | string |  |  |

