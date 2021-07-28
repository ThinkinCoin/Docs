# Protocol Interface

TRC-20 is a set of contract standards for the issuance of token assets, contracts written in compliance with this standard are considered to be a TRC-20 contract. When wallets and exchanges are docking the assets of the TRC-20 contract, from this set of standards, you can know which functions and events the contract defines, so as to facilitate the docking.

## Optional Items <a id="optional-items"></a>

Token Name

```text
string public name = "TRONEuropeRewardCoin";
```

Token Abbreviation

```text
string public symbol = "TERC";
```

Token Precision\(Decimals\)

```text
uint8 public decimals = 6;
```

## Required Items <a id="required-items"></a>

```text
contract TRC20 {             function totalSupply() constant returns (uint theTotalSupply);             function balanceOf(address _owner) constant returns (uint balance);             function transfer(address _to, uint _value) returns (bool success);             function transferFrom(address _from, address _to, uint _value) returns (bool success);             function approve(address _spender, uint _value) returns (bool success);             function allowance(address _owner, address _spender) constant returns (uint remaining);             event Transfer(address indexed _from, address indexed _to, uint _value);             event Approval(address indexed _owner, address indexed _spender, uint _value);}
```

**totalSupply\(\)** This function returns the total supply of the token.

**balanceOf\(\)** This function returns the token balance of the specific account.

**transfer\(\)** This function is used to transfer a number of tokens to a specific address.

**approve\(\)** This function is used to authorize the third party \(like a DAPP smart contract\) to transfer the token from the token owner’s account.

**transferFrom\(\)** This function is used to allow the third party to transfer the token from an owner account to a receiver account. The owner account must be approved to be called by the third party.

**allowance\(\)** This function is used to query the remaining amount of tokens the third party can transfer.

## Event Functions <a id="event-functions"></a>

When the token is successfully transferred, the contract will trigger a Transfer Event.

```text
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```

When `approval()` is successfully called, the contract will trigger an `Approval` Event.

```text
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

