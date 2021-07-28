# Create a Fixed-cap Asset

Fixed-cap assets are fungible tokens for which the supply is determined at the time of asset creation. No additional quantities can be generated afterwards.

## Create the Asset <a id="create-the-asset"></a>

### 1. Write the token smart contract <a id="1-write-the-token-smart-contract"></a>

Extension of ERC20 that adds a cap to the supply of tokens

This contract is designed to be unopinionated, allowing developers to access the internal functions in ERC20 \(such as [\_mint](https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20-_mint-address-uint256-)\) and expose them as external functions in the way they prefer. On the other hand, [ERC20 Presets](https://docs.openzeppelin.com/contracts/3.x/erc20#Presets) \(such as [ERC20PresetMinterPauser](https://docs.openzeppelin.com/contracts/3.x/api/presets#ERC20PresetMinterPauser)\) are designed using opinionated patterns to provide developers with ready to use, deployable contracts.

#### Functions <a id="functions"></a>

_Fixed-cap Assets_

* constructor\(cap\)
* cap\(\)
* \_beforeTokenTransfer\(from, to, amount\)

_General_

* name\(\)
* symbol\(\)
* decimals\(\)
* totalSupply\(\)
* balanceOf\(account\)
* transfer\(recipient, amount\)
* allowance\(owner, spender\)
* approve\(spender, amount\)
* transferFrom\(sender, recipient, amount\)
* increaseAllowance\(spender, addedValue\)
* decreaseAllowance\(spender, subtractedValue\)
* \_transfer\(sender, recipient, amount\)
* \_mint\(account, amount\)
* \_burn\(account, amount\)
* \_approve\(owner, spender, amount\)
* \_setupDecimals\(decimals\_\)

### 2. Compile your code into bytecode <a id="2-compile-your-code-into-bytecode"></a>

### 3. Deploy your Fixed-cap Asset by sending your code in a transaction to the Fantom network <a id="3-deploy-your-fixed-cap-asset-by-sending-your-code-in-a-transaction-to-the-fantom-network"></a>

### 4. Navigate to [the explorer](https://explorer.fantom.network/) to check that your token has been created <a id="4-navigate-to-the-explorer-to-check-that-your-token-has-been-created"></a>

Last updated 7 months ago

