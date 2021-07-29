# TRC-20 Event Listener

Use Tronweb's `watch` method to listen to events emitted by the smart contract method. You can set a callback function to handle the event. When the event occurs, the callback function will be triggered. The following example listens to the transfer event of the USDT-TRC20 contract of the MainNet.

**Tronweb Example:**JavaScript

```text
const trc20ContractAddress = "TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t"； //mainnet USDT contract
let contract = await tronWeb.contract().at(trc20ContractAddress);

//contract.[eventname].watch(callback) enventname is the name of the event of the contract
await contract && contract.Transfer().watch((err, event) => {
  if(err)
    return console.error('Error with "Message" event:', err);

  console.group('New event received');
  console.log('- Contract Address:', event.contract);
  console.log('- Event Name:', event.name);
  console.log('- Transaction:', event.transaction);
  console.log('- Block number:', event.block);
  console.log('- Result:', event.result, '\n');
  console.groupEnd();
});
```

