# Widget

Currently, users can't perform any actions with Binance Bridge unless their wallets are connected. This widget is meant to be used client-side to improve the flow of connecting wallets.

## Connect <a id="connect"></a>

You should see a connection request from Binance Bridge. Click on the Connect button to accept it.

![](https://lh3.googleusercontent.com/BUHkPydTlqrvXGrcc0uTmf_JItIBC0EKEjpOjZJQjhevnuDDLff-Dv37TTBG-r1vo4Icwth-p3um5FUIkElbuOmDj7hsk7ypEJkn9yx_HBvLMaTjtlN909R_VEjXK74TTMZ7UdtZ)

img

**Base URL**

​[https://www.binance.org/en/bridge?wallet=$wallet\_name](https://www.binance.org/en/bridge?wallet=$wallet_name)​

* Supported wallet name in desktop browser: MetaMask, Binance Wallet.
* Supported wallet name in mobile app browser:
  * Trust Wallet
  * MetaMask
  * Math Wallet

Example request

```text
https://www.binance.org/en/bridge?wallet=metamask
```

This URL support both MathWallet and MetaMask. Open the link in the wallet browser.

Note: please make sure the wallet is connected to Binance Smart Chain mainnet.

