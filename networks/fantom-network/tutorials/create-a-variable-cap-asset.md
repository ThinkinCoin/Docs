# Create a Variable-cap Asset

Variable-cap assets are fungible tokens for which additional quantities can be minted after creation.

 This contract is designed to be unopinionated, allowing developers to access the internal functions in ERC20 \(such as [\_mint](https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20-_mint-address-uint256-)\) and expose them as external functions in the way they prefer. On the other hand, [ERC20 Presets](https://docs.openzeppelin.com/contracts/3.x/erc20#Presets) \(such as [ERC20PresetMinterPauser](https://docs.openzeppelin.com/contracts/3.x/api/presets#ERC20PresetMinterPauser)\) are designed using opinionated patterns to provide developers with ready to use, deployable contracts.

name\(\)

symbol\(\)

decimals\(\)

totalSupply\(\)

balanceOf\(account\)

transfer\(recipient, amount\)

allowance\(owner, spender\)

approve\(spender, amount\)

transferFrom\(sender, recipient, amount\)

increaseAllowance\(spender, addedValue\)

decreaseAllowance\(spender, subtractedValue\)

\_transfer\(sender, recipient, amount\)

\_mint\(account, amount\)

\_burn\(account, amount\)

\_approve\(owner, spender, amount\)

\_setupDecimals\(decimals\_\)

