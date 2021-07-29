# TRC-721 Token Issuance

## 1 Create a TRON Account

Install the Chrome extension of [TronLink](https://www.tronlink.org/) to get ready for your issuance. You may create a new account in three ways:

* create a new account
* restoring from a mnemonic phrase, private key or Keystore
* connect to a hardware wallet

350 TRX is required in your account as the minimum.

## 2 TRC-721 Code Modification

You may modify the file of TRC721Token.sol to customise the name and symbol of the token. Remember to save your changes.

TRC-721 contract template: [template](https://developers.tron.network/docs/contract-example-1)![](https://files.readme.io/91382cc-441615884766_.pic.jpg)![](https://files.readme.io/91382cc-441615884766_.pic.jpg)

## 3 Deploy a TRC-721 Smart Contract

Deploy with tronscan: [Contract Compiler](https://tronscan.io/#/contracts/contract-compiler)

### 3.1 Connect to the Wallet

![](https://files.readme.io/e0d7ad3-451615885008_.pic.jpg)![](https://files.readme.io/e0d7ad3-451615885008_.pic.jpg)

### 3.2 Upload Contract Codes

![](https://files.readme.io/97e3263-461615885065_.pic.jpg)![](https://files.readme.io/97e3263-461615885065_.pic.jpg)![](https://files.readme.io/62b74e8-471615885081_.pic.jpg)![](https://files.readme.io/62b74e8-471615885081_.pic.jpg)

### 3.3 Compile the Contract

![](https://files.readme.io/e61fca5-481615885109_.pic_hd.jpg)![](https://files.readme.io/e61fca5-481615885109_.pic_hd.jpg)

Please choose the compiler version between 0.5.14 and 0.5.5![](https://files.readme.io/e8a29e1-491615885127_.pic.jpg)![](https://files.readme.io/e8a29e1-491615885127_.pic.jpg)

Click ‘Confirm’ to compile. Compilation succeeds with this:![](https://files.readme.io/fe42cc9-501615885142_.pic.jpg)![](https://files.readme.io/fe42cc9-501615885142_.pic.jpg)

### 3.4 Deploy the Contract

![](https://files.readme.io/82b1060-511615885169_.pic_hd.jpg)![](https://files.readme.io/82b1060-511615885169_.pic_hd.jpg)

Remember to choose TRC721Token, for it is the main contract.![](https://files.readme.io/502d573-521615885187_.pic_hd.jpg)![](https://files.readme.io/502d573-521615885187_.pic_hd.jpg)

Click Confirm to deploy. There will be a pop-up from TronLink, click Accept to sign.![](https://files.readme.io/1451dd0-531615885206_.pic_hd.jpg)![](https://files.readme.io/1451dd0-531615885206_.pic_hd.jpg)

## 4 Minting an NFT Token

Log in to Tronscan with your wallet, and use the contract address to open the deployed TRC-721 contract. Here, take the TZ4NjvdqyCbWmZxXEEAb3bXhfT8f6YGxJd contract on the Nile test net as an example:

* Choose 'Contract', 'Write Contract'

![](https://files.readme.io/68befe3-731616989680_.pic_hd.jpg)![](https://files.readme.io/68befe3-731616989680_.pic_hd.jpg)

* Find the mintWithTokenURI method, fill in the to\_address, tokenId, and the tokenURI corresponding to coral.json

![](https://files.readme.io/91e5b67-741616989852_.pic.jpg)![](https://files.readme.io/91e5b67-741616989852_.pic.jpg)

> #### 📘Metadata URI
>
> Refer to [Uploading NFT MEtadata to BTFS Network](https://developers.tron.network/docs/uploading-nft-metadata-to-the-btfs-network) for the generation of metadata URI.

* Click 'send', then accept the signature. A 'true' will be displayed if the token was mint successfully

![](https://files.readme.io/8f385c2-711616987914_.pic.jpg)![](https://files.readme.io/8f385c2-711616987914_.pic.jpg)![](https://files.readme.io/6007a35-751616990209_.pic.jpg)![](https://files.readme.io/6007a35-751616990209_.pic.jpg)

## 5 Record TRC-721 Token

Record with Tronscan: [Record tool](https://tronscan.org/#/tokens/create/Type)

* Select token type

![](https://files.readme.io/6c81294-1.png)![](https://files.readme.io/6c81294-1.png)

Select the TRC721 token and click Yes.

* Enter TRC721 token information Enter the basic information, contract address and social media information of the token. Fields with "\*" are required information. Please note that record must be logged in with the deployer address.

![](https://files.readme.io/120ef5c-2.png)![](https://files.readme.io/120ef5c-2.png)

Confirm all information required for the TRC721 token, click Submit.![](https://files.readme.io/cda6330-3.png)![](https://files.readme.io/cda6330-3.png)

You will see a popup from Tronlink asking for your signature. Click Accept to sign the message.![](https://files.readme.io/612fbab-4.png)![](https://files.readme.io/612fbab-4.png)

* Token successfully recorded

![](https://files.readme.io/a12342d-5.png)![](https://files.readme.io/a12342d-5.png)

## 6 Mobile Wallet adds TRC-721 tokens and transfer TRC-721

* Click the Add Assets button

![](https://files.readme.io/d488fb3-1.png)![](https://files.readme.io/d488fb3-1.png)

* Click the search button

![](https://files.readme.io/b6ded3a-2.png)![](https://files.readme.io/b6ded3a-2.png)

* Input TRC-721 contract address and click add button

![](https://files.readme.io/2105f04-3.png)![](https://files.readme.io/2105f04-3.png)

TRC721 added successfully![](https://files.readme.io/d7c0a14-4.png)![](https://files.readme.io/d7c0a14-4.png)

* Click TRC-721 token, for example Wendy

![](https://files.readme.io/d0dc74f-5.png)![](https://files.readme.io/d0dc74f-5.png)

* Click Wendy 721 in List collectibles

![](https://files.readme.io/3dbcbf4-6.png)![](https://files.readme.io/3dbcbf4-6.png)

* Click send for transfer TRC-721

![](https://files.readme.io/8098de2-7.png)![](https://files.readme.io/8098de2-7.png)

* Input address for receiving and enter your password for wallet

![](https://files.readme.io/879ebd7-8.png)![](https://files.readme.io/879ebd7-8.png)

* Transfer successfully

![](https://files.readme.io/92f55bb-9.png)![](https://files.readme.io/92f55bb-9.png)

