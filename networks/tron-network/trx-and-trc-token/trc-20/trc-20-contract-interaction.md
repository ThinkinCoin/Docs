# TRC-20 Contract Interaction

Take the USDT contract on Shasta test net as an example，Use Tronweb and wallet-cli to call the TRC-20 interface of the contract, respectively.

Some related links:  
[Find the USDT on Tronscan](https://shasta.tronscan.org/#/contract/TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK/code)  
[Code conversion tool](https://shasta.tronscan.org/#/tools/tron-convert-tool)

We can use the `triggersmartcontract` function to call constant functions in the contract to get the result directly without broadcasting.  
Please set `supportConstant` = true in your node config.

## name

Call the name function to get the name of the token.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST  https://127.0.0.1:8090/wallet/triggerconstantcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"name()",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use call to execute a pure or view smart contract method.
        // These methods do not modify the blockchain, do not cost anything to execute and are also not broadcasted to the network.
        let result = await contract.name().call();
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK name() # false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

## symbol

Call the symbol function to get the symbol of the token.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST  https://127.0.0.1:8090/wallet/triggerconstantcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"symbol()",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use call to execute a pure or view smart contract method.
        // These methods do not modify the blockchain, do not cost anything to execute and are also not broadcasted to the network.
        let result = await contract.symbol().call();
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK symbol() # false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

## decimals

Call the decimals function to get the precision of the token.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST  https://127.0.0.1:8090/wallet/triggerconstantcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"decimals()",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use call to execute a pure or view smart contract method.
        // These methods do not modify the blockchain, do not cost anything to execute and are also not broadcasted to the network.
        let result = await contract.decimals().call();
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK decimals() # false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

## totalSupply

Call the totalSupply function to get the total supply of the token.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST  https://127.0.0.1:8090/wallet/triggerconstantcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"totalSupply()",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use call to execute a pure or view smart contract method.
        // These methods do not modify the blockchain, do not cost anything to execute and are also not broadcasted to the network.
        let result = await contract.totalSupply().call();
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK totalSupply() # false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

## balanceOf

Call the balanceOf function to get the token balance of the specified account.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST https://127.0.0.1:8090/wallet/triggerconstantcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"balanceOf(address)",
"parameter":"000000000000000000000041977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address
    var address = "TM2TmqauSEiRf16CyFgzHV2BVxBe...";

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use call to execute a pure or view smart contract method.
        // These methods do not modify the blockchain, do not cost anything to execute and are also not broadcasted to the network.
        let result = await contract.balanceOf(address).call();
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK balanceOf(address) "TM2TmqauSEiRf16CyFgzHV2BVxBejY9iyR" false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

## transfer

Call transfer function for token transfer

**HTTP API :**HTTP

```text
wallet/triggersmartcontract
Description: Trigger smart contract
demo: curl -X POST https://127.0.0.1:8090/wallet/triggersmartcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"transfer(address,uint256)",
"parameter":"00000000000000000000004115208EF33A926919ED270E2FA61367B2DA3753DA0000000000000000000000000000000000000000000000000000000000000032",
"fee_limit":100000000,
"call_value":0,
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

The parameter is to encode address and uint256 in transfer \(address,uint256\), please refer to [the parameter encoding and decoding document](https://developers.tron.network/docs/parameter-and-return-value-encoding-and-decoding)  
Note: After calling this HTTP API, you also need to call the signature and broadcast APIs.

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address
    var address = "TM2TmqauSEiRf16CyFgzHV2BVxBe...";

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use send to execute a non-pure or modify smart contract method on a given smart contract that modify or change values on the blockchain.
        // These methods consume resources(bandwidth and energy) to perform as the changes need to be broadcasted out to the network.
        let result await contract.transfer(
            "TVDGp...", //address _to
            1000000   //amount
        ).send({
            feeLimit: 1000000
        }).then(output => {console.log('- Output:', output, '\n');});
        console.log('result: ', result);
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK  transfer(address,uint256) "TBQDyqoJ2ZJHTRDsrGQasyqBm4nUVLbWee",100 false 100000000 0 0 #
```

**Usage ：**  
TriggerContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\] \[fee\_limit\] \[value\] \[token\_value\] \[token\_id\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format  
fee\_limit: the maximum trx consumption of this calling, the unit is sun  
value: the amount of TRX that transfered to the contract while calling the contract, the unit is sun  
token\_value: the amount of TRC10 asset that transfered to the contract while calling the contract  
token\_id:the TRC10 asset ID that transfered to the contract while calling the contract

Transaction confirmation：  
Check whether the transfer of TRC20 was successful according to result of getTransactionInfoById.

## approve

Call the approve function to authorize token use rights to other addresses

**HTTP API :**HTTP

```text
wallet/triggersmartcontract
Description: Trigger smart contract
demo: curl -X POST https://127.0.0.1:8090/wallet/triggersmartcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"approve(address,uint256)",
"parameter":"0000000000000000000000410FB357921DFB0E32CBC9D1B30F09AAD13017F2CD0000000000000000000000000000000000000000000000000000000000000064",
"fee_limit":100000000,
"call_value":0,
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

Note: After calling this HTTP API, you also need to call the signature and broadcast APIs.

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    //User A allows user B to use 10USDT of A: A calls approve (B,10)
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use send to execute a non-pure or modify smart contract method on a given smart contract that modify or change values on the blockchain.
        // These methods consume resources(bandwidth and energy) to perform as the changes need to be broadcasted out to the network.
        await contract.approve(
            "TA1g2WQiXbU...", //address _spender
            10000000 //amount
        ).send({
            feeLimit: 100000000
        }).then(output => {console.log('- Output:', output, '\n');});
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK  approve(address,uint256) "TBQDyqoJ2ZJHTRDsrGQasyqBm4nUVLbWee",100 false 100000000 0 0 #
```

**Usage ：**  
TriggerContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\] \[fee\_limit\] \[value\] \[token\_value\] \[token\_id\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format  
fee\_limit: the maximum trx consumption of this calling, the unit is sun  
value: the amount of TRX that transfered to the contract while calling the contract, the unit is sun  
token\_value: the amount of TRC10 asset that transfered to the contract while calling the contract  
token\_id:the TRC10 asset ID that transfered to the contract while calling the contract

Transaction confirmation：  
Check whether the transfer of TRC20 was successful according to result of getTransactionInfoById.

## transferFrom

Calling the transferFrom function to transfer tokens from other people's accounts， needs to be used in conjunction with the approve method.

**HTTP API :**HTTP

```text
wallet/triggersmartcontract
Description: Trigger smart contract
demo: curl -X POST https://127.0.0.1:8090/wallet/triggersmartcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"transferFrom(address,address,uint256)",
"parameter":"00000000000000000000004109669733965A37BA3582E70CCC5302F8D254675D0000000000000000000000410FB357921DFB0E32CBC9D1B30F09AAD13017F2CD0000000000000000000000000000000000000000000000000000000000000032",
"fee_limit":100000000,
"call_value":0,
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

Note: After calling this HTTP API, you also need to call the signature and broadcast APIs.

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    // Address B transfers 10 USDT from address A to C: B calls transferFrom (A, C, 10)
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use send to execute a non-pure or modify smart contract method on a given smart contract that modify or change values on the blockchain.
        // These methods consume resources(bandwidth and energy) to perform as the changes need to be broadcasted out to the network.
        await contract.transferFrom(
            "TM2TmqauSEiRf16CyFgzHV2BVxBej...", //address _from
            "TVDGpn4hCSzJ5nkHPLetk8KQBtwaT...", //address _to
            100000 //amount
        ).send({
            feeLimit: 10000000
        }).then(output => {console.log('- Output:', output, '\n');});
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK  transferFrom(address,address,uint256) "TApuyuazZnGgxvbNbaGcrUijEFn1oidsAH","TBQDyqoJ2ZJHTRDsrGQasyqBm4nUVLbWee",50 false 100000000 0 0 #
```

**Usage ：**  
TriggerContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\] \[fee\_limit\] \[value\] \[token\_value\] \[token\_id\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format  
fee\_limit: the maximum trx consumption of this calling, the unit is sun  
value: the amount of TRX that transfered to the contract while calling the contract, the unit is sun  
token\_value: the amount of TRC10 asset that transfered to the contract while calling the contract  
token\_id:the TRC10 asset ID that transfered to the contract while calling the contract

Transaction confirmation：  
Check whether the transfer of TRC20 was successful according to result of getTransactionInfoById.

## allowance

Call the allowance function to query the token balance of the query account available for third-party transfers.

**HTTP API :**HTTP

```text
/wallet/triggerconstantcontract
Description: Trigger the constant of the smart contract, the transaction is off the blockchain
demo: curl -X POST https://127.0.0.1:8090/wallet/triggersmartcontract -d '{
"contract_address":"419E62BE7F4F103C36507CB2A753418791B1CDC182",
"function_selector":"allowance(address,address)",
"parameter":"00000000000000000000004109669733965A37BA3582E70CCC5302F8D254675D000000000000000000000041A245B99ECB47B18C6A90ED1D51100C5A9F0641A7",
"owner_address":"41977C20977F412C2A1AA4EF3D49FEE5EC4C31CDFB"
}'
```

**Tronweb Example:**JavaScript

```text
const TronWeb = require('tronweb')

const HttpProvider = TronWeb.providers.HttpProvider;
const fullNode = new HttpProvider("https://127.0.0.1:8090");
const solidityNode = new HttpProvider("https://127.0.0.1:8090");
const eventServer = new HttpProvider("https://127.0.0.1:8090");
const privateKey = "your private key";
const tronWeb = new TronWeb(fullNode,solidityNode,eventServer,privateKey);

async function triggerSmartContract() {
    //Query the USDT balance that Account A can use for Account B: Account B calls allowance (A, B)
    const trc20ContractAddress = "TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK";//contract address

    try {
        let contract = await tronWeb.contract().at(trc20ContractAddress);
        //Use send to execute a non-pure or modify smart contract method on a given smart contract that modify or change values on the blockchain.
        // These methods consume resources(bandwidth and energy) to perform as the changes need to be broadcasted out to the network.
        const value = await contract.allowance(
            "TM2TmqauSEiRf16CyFgzHV2BVxBejY9...", //address _owner
            "TA1g2WQiXbU5GnYBTJ5Cp22dvSjT3ug..." //address _spender
        ).call();
        console.log('- Output:', value, '\n');
    } catch(error) {
        console.error("trigger smart contract error",error)
    }
}
```

**Wallet-cli Example:**wallet-cli command

```text
TriggerConstantContract TQQg4EL8o1BSeKJY4MJ8TB8XK7xufxFBvK allowance(address,address) "TApuyuazZnGgxvbNbaGcrUijEFn1oidsAH","TQmDzierQxEFJm1dT5YXnTXqVAfdN9HtXj" false
```

**Usage :** TriggerConstantContract \[ownerAddress\] \[contractAddress\] \[method\] \[args\] \[isHex\]  
**Parameter Description：**  
ownerAddress: calller address  
contractAdress：TRC20 contract address  
method： contract function  
args：function parameters，If there is no parameter,use \# placeholder  
isHex： whether the address of the command parameter is in hex format

