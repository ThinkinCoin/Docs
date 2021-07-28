# TRC-10 Transfer in Smart Contracts

Compared to TRC-20 tokens, TRC-10 tokens face a user experience flexibility issue. In Odyssey 3.2, developers and their smart contract callers can interact with TRC-10 token via smart contracts according to the contract logic, do TRC-10 token transfers in smart contracts, giving them more control to implement their token in business scenarios. Unlike TRC-20 tokens, sending TRC-10 tokens is like transferring TRX in a contract, TRON developers added an interface specifically for TRC-10 transfers and queries in solidity.

**Example of transferring trc10 in a contract**Solidity

```text
pragma solidity ^0.5.0;​contract transferTokenContract {    constructor() payable public{}​    function() payable external {}​    function transferTokenTest(address payable toAddress, uint256 tokenValue, trcToken id) payable public    {        toAddress.transferToken(tokenValue, id);    }​    function msgTokenValueAndTokenIdTest() public payable returns(trcToken, uint256){        trcToken id = msg.tokenid;        uint256 value = msg.tokenvalue;        return (id, value);    }​    function getTokenBalanceTest(address accountAddress) payable public returns (uint256){        trcToken id = 1000001;        return accountAddress.tokenBalance(id);    }}
```

**TRC10 token type** Odyssey\_v3.2 defined a new type \(trcToken\) for TRC10 token, which represents the tokenId in a token transfer operation. TRC10 token can be converted to uint256 type and vice versa.

**TRC10 transfer in contract**

```text
address.transferToken(uint256 tokenValue, trcToken tokenId)
```

**Query the TRC10 balance in the contract**

```text
address.tokenBalance(trcToken) returns(uint256 tokenAmount)
```

Odyssey\_v3.2 defines a new tokenBalance function for TRC10 token balance query.

**TokenValue & TokenID** Msg.tokenvalue, represents the token value in the current msg call, with a default value of 0. Msg.tokenid, represents the token id in current msg call, with a default value of 0.

