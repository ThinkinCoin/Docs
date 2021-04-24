# Oracle Module

## Oracle on Binance Chain <a id="oracle-on-binance-chain"></a>

The **oracle** module is a common module like gov which is used to handle prophecy and claim. Prophecy means the validators want to reach a consensus on something, like cross chain transfer. Claim is raised by a validator and the content of claim is the the cross chain transfer. When most of the validators \(like 70%\) claim the same thing on the prophecy, the winning claim will be executed.For oracle module is a common module, other module which depends on oracle module will register claim type and related hooks checking and handling claim. Each claim type has a sequence, oracle module should process prophecy and claim by sequence. When one prophecy was executed successfully, the sequence of the claim type will be increased by one.

### Oracle Process <a id="oracle-process"></a>

1. Oracle module receives a claim message from validator, if the sequence is not current sequence, the claim message will be rejected.
2. If sequence is valid, the hooks of the claim type will check the claim message, if the claim message is invalid, then return
3. If claim message is valid and it’s the first claim, the related prophecy will be created. If claim message is not the first claim, then it will be added to the existed prophecy.
4. If the power of validators which claim the same content reaches a threshold like 70%, the prophecy will be marked success and the hooks will executed the winning claim. and the sequence of claim type will be increased.
5. If there is no chance that the validators will reach a consensus, the prophecy will be marked failed and the prophecy will be deleted and the validators should start over again.

### Bridge Module <a id="bridge-module"></a>

Bridge module will process cross chain transactions. It contains two parts: transactions from bc to bsc and transactions from bsc to bc. For transactions from bsc to bc, it will depend on the oracle module. When the validators reach a consensus on a certain claim, the bridge module will process the transaction according to the claim, like transfer from bsc to bc. For transactions from bc to bsc, it will process the bc part of the transaction and write the related cross chain package for bsc.

