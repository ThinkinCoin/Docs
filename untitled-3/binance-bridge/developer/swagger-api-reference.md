# Swagger API reference

API description for swap service

**Version:** V1.0

**Contact information:** Binance Chain

**Base URL:** api.binance.org/bridge

**Rate Limit:** 2000 request per IP per 5 mins.

### /api/v1/tokens <a id="api-v-1-tokens"></a>

**GET**

**Summary:** get

**Parameters**

**Responses**

### /api/v1/tokens/{symbol}/networks <a id="api-v-1-tokens-symbol-networks"></a>

**GET**

**Summary:** get

**Parameters**

**Responses**

### /api/v1/swaps <a id="api-v-1-swaps"></a>

**GET**

**Summary:** find swap

**Parameters**

**Responses**

**POST**

**Summary:** create

**Parameters**

**Responses**

### /api/v1/swaps/{swapId} <a id="api-v-1-swaps-swapid"></a>

**GET**

**Summary:** get

**Parameters**

**Responses**

### /api/v1/swaps/{swapId}/email <a id="api-v-1-swaps-swapid-email"></a>

**PUT**

**Summary:** create Email

**Parameters**

**Responses**

### /api/v1/swaps/quota/24hour <a id="api-v-1-swaps-quota-24-hour"></a>

**GET**

**Summary:** getQuota

**Parameters**

**Responses**

### /api/v2/swaps <a id="api-v-2-swaps"></a>

**GET**

**Summary:** find swap V2

**Parameters**

**Responses**

**POST**

**Summary:** createV2

**Parameters**

**Responses**

### /api/v2/tokens <a id="api-v-2-tokens"></a>

**GET**

**Summary:** getQuota

**Responses**

### /api/v2/tokens/{symbol}/networks <a id="api-v-2-tokens-symbol-networks"></a>

**GET**

**Summary:** get

**Parameters**

**Responses**

## Models <a id="models"></a>

### EmailUpdateRequest <a id="emailupdaterequest"></a>

### ResponseStatus <a id="responsestatus"></a>

### ResponseStatusBodySwapCreation <a id="responsestatusbodyswapcreation"></a>

### ResponseStatusBodySwapDetail <a id="responsestatusbodyswapdetail"></a>

### SwapCreation <a id="swapcreation"></a>

### SwapCreationRequest <a id="swapcreationrequest"></a>

### SwapDetail <a id="swapdetail"></a>

### ResponseStatusBodySwapList <a id="responsestatusbodyswaplist"></a>

### SwapList <a id="swaplist"></a>

### TokenList <a id="tokenlist"></a>

### TokenListV2 <a id="tokenlistv2"></a>

### TokenDetail <a id="tokendetail"></a>

### TokenDetailV2 <a id="tokendetailv2"></a>

### NetworkList <a id="networklist"></a>

### NetworkDetail <a id="networkdetail"></a>

### NetworkListV2 <a id="networklistv2"></a>

### NetworkDetailV2 <a id="networkdetailv2"></a>

### ResponseStatusBodyQuota <a id="responsestatusbodyquota"></a>

### Quota <a id="quota"></a>

### SwapCreationRequestV2 <a id="swapcreationrequestv2"></a>

