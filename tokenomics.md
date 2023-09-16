# Tokenomics

Think in Coin ($NEURONS) is carefully structured with a deflationary model and fee distribution mechanism to ensure its stability, value appreciation, and support for the ecosystem.\


Name: Think in Coin

Ticker: $NEURONS

Total Supply: 10 million ($NEURONS)

Deflationary Rate: 0.35% per transaction



Fees:

Liquidity Fee: 0.25% per transaction, allocated to liquidity pool

Treasury Fee: 0.5% per transaction, directed to the project treasury

Smart Contract Details (Solidity):

\


`contract ThinkinCoinToken is ERC20, Ownable {`

&#x20;   `address public constant DEAD = 0x000000000000000000000000000000000000dEaD;`

&#x20;   `address public constant ZERO = 0x0000000000000000000000000000000000000000;`

&#x20;   `address public treasuryWallet;`

&#x20;   `address public liquidityWallet;`

\


&#x20;   `uint256 public constant TREASURY_FEE = 50; // 0.5%`

&#x20;   `uint256 public constant LIQUIDITY_FEE = 25; // 0.25%`

&#x20;   `uint256 public constant BURN_RATE = 35; // 0.35%`

&#x20;   `uint256 public constant TOTAL_SUPPLY = 10000000 * (10 ** 18); // 10 million tokens, scaled by 18 decimal places`

\


&#x20;   `// Rest of the contract details and functionalities...`

`}`

\


In this model, with every transaction, a portion of $NEURONS is burned, contributing to its deflationary nature. Additionally, fees from transactions are allocated to the liquidity pool and project treasury, ensuring liquidity and sustainability for the ecosystem. Think in Coin's deflationary approach and fee distribution aim to maintain long-term value and support the growth of the platform and its community.

\
