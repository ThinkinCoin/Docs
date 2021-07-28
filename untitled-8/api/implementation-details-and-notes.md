# Implementation Details and Notes

## Rewards Estimation <a id="rewards-estimation"></a>

Estimated rewards calculation uses the current status of the blockchain to approximate amount of FTM tokes rewarded for participating in staking. The network uses proof of stake consensus variant to ensure security of the data inside the blockchain structure.

To calculate the rewards we use `baseRewardPerSecond` value of the latest sealed epoch, but the total staked amount of tokens is calculated elsewhere. The epoch does provide a value of total self-staked tokens in that epoch and also the amount of total delegated tokens, but the first value does not contain temporarily offline nodes and, on the other hand, it includes delegated stake in un-delegation. That means the value is not correct for our calculations.

To get the current total staked value, we iterate all the staking records and collect total staked amount from individual staking.

## Delegation Limits <a id="delegation-limits"></a>

Delegation limit is calculated from the current self staked amount of a staker by multiplying it by fixed rate, specified in SFC contract. The current value of maximum allowed delegations is 15 times the amount of self staked FTMs.

When we calculate remaining allowed limit, the current delegated amount is subtracted from the total imit. The value is provided by API so you don't have to deal with the calculation yourself. Please note that tokens in un-delegation does not count towards `delegatedMe` value and so they don't count towards spent limit of delegations.

​

