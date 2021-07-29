# Committee and Proposal

## Committee

The committee can modify the TRON network parameters, like transaction fees, block producing reward amount, etc. Committee is composed of the current 27 super representatives. Every super representative has the right to start a proposal. The proposal will be passed after it gets more than 19 approves and will become valid in the next maintenance period.

## Proposal

Only SRs, Partners and Candidates can create a proposal.  
The network parameters can be modified\(\[min, max\]\).  
{0,1}: 1 means 'allowed' or 'actived', 0 means no.

| \# | Command | Value |
| :--- | :--- | :--- |
| 0 | getMaintenanceTimeInterval \(To modify the maintenance interval of SR\) | 6 Hours \[3 _27, 24_ 3600\] s |
| 1 | getAccountUpgradeCost \(To modify the cost of applying for SR account\) | 9999 TRX \[0, 100000000000\] TRX |
| 2 | getCreateAccountFee \(To modify the account creation fee\) | 0.1 TRX \[0, 100000000000\] TRX |
| 3 | getTransactionFee \(To modify the amount of TRX used to gain extra bandwidth\) | 40 Sun/Byte \[0, 100000000000\] TRX |
| 4 | getAssetIssueFee \(To modify asset issuance fee\) | 1024 TRX \[0, 100000000000\] TRX |
| 5 | getWitnessPayPerBlock \(To modify SR block generation reward\) | 16 TRX \[0, 100000000000\] TRX |
| 6 | getWitnessStandbyAllowance \(To modify the rewards given to the top 27 SRs and the following 100 partners\) | 115200 TRX \[0, 100000000000\] TRX |
| 7 | getCreateNewAccountFeeInSystemContract \(To modify the cost of account creation\) | 0 TRX |
| 8 | getCreateNewAccountBandwidthRate \(To modify the consumption of bandwith of account creation\) | 1 Bandwith/Byte |
| 9 | getAllowCreationOfContracts \(To activate the Virtual Machine \(VM\)\) | 1 {0, 1} |
| 10 | getRemoveThePowerOfTheGr \(To remove the GR Genesis votes\) | 1 {0, 1} |
| 11 | getEnergyFee \(To modify the fee of 1 energy\) | 40 Sun \[0, 100000000000\] TRX |
| 12 | getExchangeCreateFee \(To modify the cost of trading pair creation\) | 1024 TRX \[0, 100000000000\] TRX |
| 13 | getMaxCpuTimeOfOneTx \(To modify the maximum execution time of one transaction\) | 80 ms \[0, 1000\] ms |
| 14 | getAllowUpdateAccountName \(To allow to change the account name\) | 0 {0, 1} |
| 15 | getAllowSameTokenName \(To allow the same token name\) | 1 {0, 1} |
| 16 | getAllowDelegateResource \(To allow resource delegation\) | 1 {0, 1} |
| 18 | getAllowTvmTransferTrc10 \(To allow the TRC-10 token transfer in smart contracts\) | 1 {0, 1} |
| 19 | getTotalEnergyCurrentLimit \(To modify current total energy limit\) | 50000000000 |
| 20 | getAllowMultiSign \(To allow the initiation of multi-signature\) | 1 {0, 1} |
| 21 | getAllowAdaptiveEnergy \(To allow adaptive adjustment for total Energy\) | 0 {0, 1} |
| 22 | getUpdateAccountPermissionFee \(To modify the fee for updating account permission\) | 100 TRX |
| 23 | getMultiSignFee \(To modify the fee for multi-signature\) | 1 TRX |
| 24 | getAllowProtoFilterNum \(To enable protocol optimization\) | 0 {0, 1} |
| 26 | getAllowTvmConstantinople \(To support the new commands of Constantinople\) | 1 {0, 1} |
| 27 | getAllowShieldedTransaction \(To enable shielded transaction\) | 0 {0, 1} |
| 28 | getShieldedTransactionFee \(To modify shielded transaction fee\) | 10 TRX \[0, 10000\] TRX |
| 29 | getAdaptiveResourceLimitMultiplier \(To modify the adaptive energy limit multiplier\) | 1000 \[1, 10000\] |
| 30 | getChangeDelegation \(Propose to support the decentralized vote dividend\) | 1 {0, 1} |
| 31 | getWitness127PayPerBlock \(Propose to modify the block voting rewards given to the top 27 SRs and the following 100 partners\) | 160 TRX \[0, 100000000000\] TRX |
| 32 | getAllowTvmSolidity059 \(To allow TVM to support solidity compiler 0.5.9\) | 0 {0, 1} |
| 33 | getAdaptiveResourceLimitTargetRatio \(To modify the target energy limit\) | 10 \[1, 1000\] |

### Create a Proposal

Example \(Using wallet-cli\):Shell

```text
createproposal id value  
id: the serial number (0 ~ 18)  
value: the parameter value
```

> #### 📘Note
>
> * In TRON network, 1 TRX = 1000\_000 SUN

### Vote for a Proposal

Proposal only support YES vote. Since the creation time of the proposal, the proposal is valid within 3 days. If the proposal does not receive enough YES votes within the period of validity, the proposal will be invalid beyond the period of validity. Yes vote can be cancelled.

Example \(Using wallet-cli\):Shell

```text
approveProposal id is_or_not_add_approval
id: proposal id  
is_or_not_add_approval: YES vote or cancel YES vote
```

### Cancel Proposal

Proposal creator can cancel the proposal before it is passed.  
Example \(Using wallet-cli\):Shell

```text
deleteProposal id
id: proposal id
```

### Query Proposal

[List Proposals Full Node HTTP API](https://developers.tron.network/reference#walletlistproposals)

[List Proposals TronWeb API](https://developers.tron.network/reference#listproposals)

[Get Proposal by ID Full Node HTTP API](https://developers.tron.network/reference#walletgetproposalbyid)

