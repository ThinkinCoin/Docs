# Issuing TRC-20 tokens tutorial

## 1. Install TronLink Chrome plugin

Address: [TronLink](https://chrome.google.com/webstore/detail/tronlink%EF%BC%88%E6%B3%A2%E5%AE%9D%E9%92%B1%E5%8C%85%EF%BC%89/ibnejdfjmmkpcnlpebklmnkoeoihofec)

### **2. Prepare an account for issue token**

There are three ways to _create an account_, _import an account_, and _link a hardware wallet._ You need to ensure that there are more than 1000 TRX in the account.![](https://files.readme.io/f4260b0-_1.png)![](https://files.readme.io/f4260b0-_1.png)

### **3. Prepare the TRC20 contract code**

Trc20 contract template: [code](https://github.com/zyumingfit/TRC20-Contract-Template)

Modify the Token.sol file to define the **token name,** **token symbol**, **precision**, and **totalsupply**![](https://files.readme.io/051aee0-_1.png)![](https://files.readme.io/051aee0-_1.png)

### **4. Deploy TRC20 contract**

Deploy with tronscan: [deployment tool](https://tronscan.io/#/contracts/contract-compiler)

* Link wallet

![](https://files.readme.io/5c3df2f-_2020-08-21_12.15.55.png)![](https://files.readme.io/5c3df2f-_2020-08-21_12.15.55.png)

* Upload contract code

![](https://files.readme.io/9118251-_1.png)![](https://files.readme.io/9118251-_1.png)![](https://files.readme.io/e124c71-_1.png)![](https://files.readme.io/e124c71-_1.png)

* Compile the contract Please select 0.5.10 version compiler

![](https://files.readme.io/9ec0d79-_1.png)![](https://files.readme.io/9ec0d79-_1.png)![](https://files.readme.io/ca81448-_1.png)![](https://files.readme.io/ca81448-_1.png)

The following prompt appears, indicating successful compilation![](https://files.readme.io/7a87419-_1.png)![](https://files.readme.io/7a87419-_1.png)

* Deployment contract

Please note that you must choose the Token contract, because Token is the main contract![](https://files.readme.io/5096e27-_1.png)![](https://files.readme.io/5096e27-_1.png)

Click Confirm to deploy, the tronlink signature dialog box will pop up, click to accept to sign,when successful deployment, please get the contract address, and record the contract address.![](https://files.readme.io/956aadd-WX20200821-1210532x.png)![](https://files.readme.io/956aadd-WX20200821-1210532x.png)![](https://files.readme.io/42e3cde-_1.png)![](https://files.readme.io/42e3cde-_1.png)

### **5. Add tokens to Tronlink**

On the asset management page, fill in the contract address obtained after successful deployment in the add token input box, the contract just deployed will pop up, click the switch button, and add the token to tronlink. After the addition is successful, the transfer can be carried out.![](https://files.readme.io/26beafe-_1.png)![](https://files.readme.io/26beafe-_1.png)

You can also search the contract homepage on tronscan![](https://files.readme.io/180b061-_1.png)![](https://files.readme.io/180b061-_1.png)

### **6.Verify TRC20 contracts**

Verify with Tronacan: [Validation tool](https://tronscan.org/#/contracts/verify)

* Enter contract information including contract address,contract name, compiler version, License, optimization history and Runs.

Contract address is the address recorded while deploying the contract.  
Contract name refers to the name of the main contract deployed. In the example above, the name is "Token".  
Compiler version is 0.5.10  
You may select None for License  
Optimization history is Yes and Runs is 0 by default.![](https://files.readme.io/54a2b0b-11.png)![](https://files.readme.io/54a2b0b-11.png)

Click Upload contract file\(s\) for validation.

* Upload contract code Check I am not a robot \(Note: Google authentication is required for this step. Users in Mainland China may have to use VPN\).

![](https://files.readme.io/4106456-12.png)![](https://files.readme.io/4106456-12.png)

Click Verify and publish, you will be directed to the contract information page once validated successfully.

* Contract successfully validated Contract information page will show successful validation.

![](https://files.readme.io/842e8d2-13.png)![](https://files.readme.io/842e8d2-13.png)

### **7. Record TRC20 Token**

Record with Tronscan: [Record tool](https://tronscan.org/#/tokens/create/Type)

* Select token type

![](https://files.readme.io/19aa7aa-14.png)![](https://files.readme.io/19aa7aa-14.png)

Select the TRC20 token and click Yes.

* Enter TRC20 token information Enter the basic information, contract information and social media information of the token. Fields with "\*" are required information. The information you entered must match that of the TRC20 contract. Please note that record must be logged in with the deployer address.

![](https://files.readme.io/152689c-15.png)![](https://files.readme.io/152689c-15.png)

Enter all information required for the TRC20 token, click Next.![](https://files.readme.io/e27e3d2-16.png)![](https://files.readme.io/e27e3d2-16.png)

* Confirm token information

Check if token information is right. Click I’m not a robot, and then click Submit \(Note: Google authentication is required for this step. Users in Mainland China may have to use VPN\).![](https://files.readme.io/d8a03d1-17.png)![](https://files.readme.io/d8a03d1-17.png)

You will see a popup dialog to confirm token issuance. Click Confirm and you will see another popup from Tronlink asking for your signature. Click Accept to sign the message.![](https://files.readme.io/5ba592e-18.png)![](https://files.readme.io/5ba592e-18.png)

* Token successfully recorded

![](https://files.readme.io/c476df0-19.png)

