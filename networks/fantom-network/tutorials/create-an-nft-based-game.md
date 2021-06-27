# Create an NFT-based Game

Non-Fungible Tokens, or NFTs in short, have recently gained significant popularity due to the rising trend in the blockchain gaming space. Ever since their inception, NFTs became really popular among the crypto community, thanks to successful projects like Cryptokitties and CryptoPunks, etc.

Cryptokitties is one of the most hyped NFT projects within the DeFi and blockchain gaming space. CryptoKitties are digital, collectible cats built on the Ethereum blockchain, and they can be bought and sold using Ethereum, and bred to create new cats with several traits and varying characteristics.

CryptoKitties is basically a digital pet community centred around collecting, training, raising, and battling fantasy creatures that are known as ‘CryptoFantom’. Each CryptoFantom has unique genetic data stored on Opera.

A CryptoFantom can possess two different genes with different body parts. This smart contract serves as an example, and can be a good starting point for anyone who is looking to build NFT based products on the Fantom blockchain platform.

## Prerequisite <a id="prerequisite"></a>

To Run these examples please follow the following steps:

**Install Truffle:**

**Clone the project:**

```text
$ git clone https://github.com/Fantom-foundation/crypto-fantom-game.git
```

This project is for test purpose only, it contains only the basic functions and minimum requirements.

run `npm install` to install dependencies

```text
  Contract: Game    ✓ should NOT mint if not admin (47ms)    ✓ should mint if admin (154ms)    ✓ should NOT transfer if balance is 0 (104ms)    ✓ should NOT transfer if not owner (79ms)    ✓ safeTransferFrom() should NOT transfer if recipient contract does not implement erc721recipient interface (95ms)    ✓ transferFrom() should transfer (70ms)    ✓ transferFrom() should transfer (70ms)    ✓ safeTransferFrom() should transfer (62ms)    ✓ should transfer token when approved (117ms)    ✓ should transfer token when approved (87ms)​  Contract: Game    ✓ should NOT mint if not admin    ✓ should mint if admin (161ms)    ✓ should breed (167ms)​  13 passing (4s)
```

## Deploy Locally and Interact with frontend <a id="deploy-locally-and-interact-with-frontend"></a>

Start by running Ganache-CLI. It runs a personal Ethereum _blockchain_ on which you can use to _run_ tests, _execute_ commands. Run this command:

```text
$ ganache-cli --deterministic -i 1337
```

You should get this output:

```text
Ganache CLI v6.10.0-beta.2 (ganache-core: 2.11.0-beta.0)​Available Accounts==================(0) 0x90F8bf6A479f320ead074411a4B0e7944Ea8c9C1 (100 ETH)(1) 0xFFcf8FDEE72ac11b5c542428B35EEF5769C409f0 (100 ETH)(2) 0x22d491Bde2303f2f43325b2108D26f1eAbA1e32b (100 ETH)(3) 0xE11BA2b4D45Eaed5996Cd0823791E0C93114882d (100 ETH)(4) 0xd03ea8624C8C5987235048901fB614fDcA89b117 (100 ETH)(5) 0x95cED938F7991cd0dFcb48F0a06a40FA1aF46EBC (100 ETH)(6) 0x3E5e9111Ae8eB78Fe1CC3bb8915d5D461F3Ef9A9 (100 ETH)(7) 0x28a8746e75304c0780E011BEd21C72cD78cd535E (100 ETH)(8) 0xACa94ef8bD5ffEE41947b4585a84BdA5a3d3DA6E (100 ETH)(9) 0x1dF62f291b2E969fB0849d99D9Ce41e2F137006e (100 ETH)​......Listening on 127.0.0.1:8545
```

You can either import the mnemonic into metamask or at least the first account \(you should have the private key\) into Metamask.

![](https://gblobscdn.gitbook.com/assets%2F-MKjpUMrhoyibSIWfRrl%2F-MPA6Y_NtcbEzXpraLY0%2F-MPFFn34rOaQaSSZsCaq%2FScreenshot%202020-12-23%20at%2016.32.18.png?alt=media&token=1aa25d8e-86a1-451e-a665-4003aaf9d9af)

Add local network to Metamask

Then deploy our contract by running this command:

```text
$ truffle migrate --network testrpc --reset
```

You should get this output:

```text
Compiling your contracts...===========================✔ Fetching solc version list from solc-bin. Attempt > Everything is up to date, there is nothing to compile.​​​Starting migrations...======================> Network name:    'testrpc'> Network id:      1337> Block gas limit: 6721975 (0x6691b7)​​1_initial_migration.js======================​   Replacing 'Migrations'   ----------------------   > transaction hash:    0x28099872c6feeceab4033e63e9a3c48e73f315e2c61feef4a5bf7ac947c3329e   > Blocks: 0            Seconds: 0   > contract address:    0xe78A0F7E598Cc8b0Bb87894B0F60dD2a88d6a8Ab   > block number:        1   > block timestamp:     1608736619   > account:             0x90F8bf6A479f320ead074411a4B0e7944Ea8c9C1   > balance:             99.99665588   > gas used:            167206 (0x28d26)   > gas price:           20 gwei   > value sent:          0 ETH   > total cost:          0.00334412 ETH​​   > Saving migration to chain.   > Saving artifacts   -------------------------------------   > Total cost:          0.00334412 ETH​​2_deploy_contracts.js=====================​   Replacing 'CryptoFantom'   ------------------------   > transaction hash:    0x8a3dd0bc5d57a8f6dcba777ded4b0a2038fe6f8c7c6684e8546cd49a40220a9d   > Blocks: 0            Seconds: 0   > contract address:    0xCfEB869F69431e42cdB54A4F4f105C19C080A601   > block number:        3   > block timestamp:     1608736619   > account:             0x90F8bf6A479f320ead074411a4B0e7944Ea8c9C1   > balance:             99.9661064   > gas used:            1485231 (0x16a9af)   > gas price:           20 gwei   > value sent:          0 ETH   > total cost:          0.02970462 ETH​​   > Saving migration to chain.   > Saving artifacts   -------------------------------------   > Total cost:          0.02970462 ETH​​Summary=======> Total deployments:   2> Final cost:          0.03304874 ETH
```

Then you can finally run:

```text
Compiled successfully!​You can now view app in the browser.​  Local:            http://localhost:3000/  On Your Network:  http://192.168.102.7:3000/​Note that the development build is not optimized.To create a production build, use npm run build.​
```

## Issues <a id="issues"></a>

You may encounter some problems with the current version of Metamask which does not detect the correct nonce, you can switch from network to Mainnet and then back to Local that solves most of the issues until a correction is made.

​

