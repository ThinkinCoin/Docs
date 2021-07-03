# Mechanism

## Election

Every account in the TRON network has the right to vote for SRs candidates. TRON Power \(TP\) is required to vote, and the amount of TP depends on the voter’s frozen assets\(TRX\), 1 TP = 1 frozen TRX.

An account loses the TP after release\(unfreeze\) the frozen TRX, and votes for the ongoing and future round are invalid unless freeze TRX to get TP again.

Note that the TRON network only records your most recent vote, every new vote overwrites the old one.

Votes are counted every 6 hours. The top 27th are called super representatives, 28th-127th are super partners, after 128th are super representative candidates.

TRON network burns 9999 TRX from the account that applies to become a super representative candidate to prevent attacks.

## Rewards

1. **Super Representative Reward\(Block Reward\):** The TRON network generates block every 3 seconds, with each block awarding 16 TRX to Super Representatives.
2. **Candidate Reward\(Vote Reward\):** With every block producing, the top 127 share 160 TRX. The reward will be split by the votes each candidate receives. The voting rewards obtained by super representatives and partners will also be distributed to voters in accordance with the voting ratio of voters after deducting the commission ratio.

Each time a Super Representative finishes block production, rewards are sent to the sub-account in the superledger. Super Representatives can check, but not directly make use of this asset. A withdrawal can be made every 24 hours, transferring the reward from the sub-account to the Super Representative’s account.

### Rewards Calculation

**Total Rewards = Vote Reward** _**x**_ **brokerage ratio+ Block Reward** _**x**_ **brokerage ratio**

_**Super representative brokerage**_

The default ratio is 20%, and the other 80% will be awarded to the voters. The ratio can be modified by the super representative.

_**Vote Rewards**_

* Vote rewards are 160 TRX every block.
* Voting statistics counted every 6 hours, with SRs changing based on vote results.
* For all 127 SR individuals, the vote rewards per day are calculated as follows: 160 \(TRX/block\) _x_ 7200 \(blocks/election\) _x_ 4 \(elections/day\) = 4,608,000 \(TRX/day\)2.
* For each candidate, the daily Vote Rewards = 4,608,000 _x_ \(\# votes / \# total votes\) _x_ 20%

2_Reward may be less than the theoretical number due to missed blocks._

_**Block Rewards**_

* SRs create blocks one by one and block rewards are 16 TRX every block.
* Block rewards per day: 16 \(TRX/block\) _x\_7200 \(blocks/election\) \_x_ 4 \(elections/day\) = 460,800 \(TRX/Day\) For each super representative, the daily Block Rewards = 460,800/27 _x_ 20%

_**Voter Rewards**_

* Calculated by default brokerage ratio, 80% of the rewards are distributed to his voters, and each vote corresponds to a reward of 6 hours = 80% x 7200 \(block/election\) x 160 /total votes + 80% x 7200 \(blocks/election\) x 16 / 27 / sr votes\). 'Total votes' is the total number of votes for the entire network, and 'SR votes' is the number of votes the super partner receives. Therefore, each voter needs to know the brokerage ratio, total votes and sr votes to calculate the reward, and this data is open to everyone.

_**Take one of the top 27 super representatives as an example:**_![](https://files.readme.io/f8709d3-00f9739-Foxmail20191101105016.png)![](https://files.readme.io/f8709d3-00f9739-Foxmail20191101105016.png)

Vote Rewards: 4,608,000 _x_ 2.19% x 20% = 20,183 TRX  
Block Rewards: 460,800 / 27 _x_ 20% = 34,13 TRX  
Total Rewards: 20183 + 3413 = 23596 TRX  
This SR receives about 23596 TRX total rewards per day.  
Voter Rewards:  
votes _x_ 80% _x_ 28800\(blocks/day\) _x_（ 160/ total votes + 16 / 27 _x_（votes / sr votes））

_**Take one of the super representative candidate from 28 to 127 as an example**_![](https://files.readme.io/de25852-c41a9cf-Foxmail20191101113132.png)![](https://files.readme.io/de25852-c41a9cf-Foxmail20191101113132.png)

Vote Rewards: 4,608,000 x 1.09% x 20%= 10045 TRX  
Block Rewards: 0TRX  
Total Rewards: 10045 + 0 = 10045 TRX  
This SR receives about 10045 TRX total rewards per day.  
Voter Rewards:  
votes _x_ 80% _x_ 28800\(blocks/day\) \_x\_160/ total votes

For estimating SR voting reward and SR rank by specific votes amount, please use [**TRON Station**](https://tronstation.io/votereward) voting reward tool to calculate.

Users can use the blockchain explorer [https://tronscan.org](https://tronscan.org/) to get SR information.  
SR information is as follows :

* Delegate's account address
* Total votes the delegate received
* Delegate's website url
* Total number of blocks produced by the delegate
* The total missed blocks of delegate

## API

[Update brokerage](https://developers.tron.network/reference-link/update-brokerage)

[Query SR brokerage ratio](https://developers.tron.network/reference#query-sr-brokerage-ratio)

[Query user reward](https://developers.tron.network/reference#get-user-voting-rewards)

[Withdraw balance](https://developers.tron.network/reference-link/walletwithdrawbalance-1)

