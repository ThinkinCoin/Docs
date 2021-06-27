# EasyStaking on Ethereum

## EasyStaking <a id="easystaking"></a>

​☑ [https://easy-staking.xdaichain.com/deposits](https://easy-staking.xdaichain.com/deposits)​

## What is Easy Staking? <a id="what-is-easy-staking"></a>

Easy Staking allows users to place STAKE into a contract and receive STAKE emissions on Ethereum. It provides an accessible staking mechanism for users and increases STAKE utility and DeFi composability. EasyStaking also:

* Incentivizes liquidity providers on decentralized exchanges through unique reward mechanisms
* Creates staking opportunities via hardware wallets and other Ethereum applications
* Provides staking opportunities with no minimum STAKE requirements to participate
* Limits total circulating supply

Total STAKE Emissions are minted at a total of 15% APR. Emissions are sent to stakers as well as Liquidity Pool Providers \(see below\) and provisioned based on two parameters:

* **Time**: 7.5% APR. The amount of time STAKE has been committed to the protocol. Longer staking times result in a higher APR for the Staker.
* **Total Staked Amount**: 7.5% APR. The total amount in the pool from all Stakers and other contributors. Larger stakes result in a higher APR for all Stakers. More staked amount = higher rewards.

![](https://gblobscdn.gitbook.com/assets%2F-Lpi9AHj62wscNlQjI-l%2F-MDxTJDSDPIIWj0CFhVO%2F-MDxVj1L9TOjMXldEun_%2FSigmoid_With_Parameters.png?alt=media&token=a7521fc6-a29d-4aac-9708-87757c873109)

Sigmoid function for determining time-based APR.

Stakers and Liquidity Providers each receive portions of the emission based on how long a Staker decides to keep STAKE in the application and the total amount Staked. Longer staking times benefit the Staker, and shorter staking periods benefit Liquidity Providers.

## Time-Based Emission Example <a id="time-based-emission-example"></a>

As well as functioning as a stand-alone application, Easy Staking may be integrated into hardware wallets and other applications.

## Liquidity Pool \(LP\) Participants <a id="liquidity-pool-lp-participants"></a>

LP incentives are distributed on average every 7 days - the exact distribution date is randomized. Incentives are distributed among the **top 100 pools**.

* * 
Liquidity pool providers will also receive STAKE incentives from the Easy Staking application. Users who put funds into an ETH/STAKE liquidity pool on Uniswap will be eligible for these additional incentives. **Note only the top 100 LPs receive additional STAKE.**

 Here's an example of how it works for 👨🌾 Bob:

1. Bob acquires .3 ETH and 30 STAKE by trading on [Uniswap](https://uniswap.exchange/swap), purchasing on [BitMax](https://bitmax.io/), or through some other means. \(Model assumes .3 ETH and 30 STAKE have equivalent value\)
2. He goes to Uniswap \(v2\) and adds both into the [STAKE/ETH liquidity pool](https://uniswap.info/pair/0x3B3d4EeFDc603b232907a7f3d0Ed1Eea5C62b5f7).
3. After some time, 👨🌾 Bob checks his address and sees that he has received an additional 51 STAKE directly to his wallet. He has received STAKE rewards \(at a very high % relative to his pool contribution\) thanks to 👩🎨 Mary ⤵ withdrawing money from Easy Staking.

## STAKE Distribution \(time-based example\) <a id="stake-distribution-time-based-example"></a>

​👩🎨 Mary has 10,000 STAKE she places into the Easy Staking application on the Ethereum Mainnet. She submits a deposit through the Easy Staking UI. After 1 year, she decides to realize her STAKE gains and submits a withdrawal request. Assume APR is 10%. Since she deposited 10000 STAKE and staked for 1 year, Mary receives 11000 STAKE \(her initial amount + 10% APR\). The remaining 500 STAKE \(5% APR\) earned as part of the total 15% APR are sent to the LP distribution contract.

Distribution to LP participants occurs through a script which collects addresses and pool amounts. It is called once a week \(within 5-9 day time slots at random intervals\) and distributes funds based on pool participation percentages.

For simplicity, let's say only 👨🌾 Bob and 👨🍳 Roger were participating in the Uniswap LP. Bob has .3 ETH/30 STAKE and Roger has .1 ETH/10 STAKE in the pool when the distribution script is executed. At this point, 👨🌾 Bob receives 375 STAKE \(75% of the STAKE in the LP distribution contract\) and 👨🍳 Roger 125 STAKE \(25%\) based on 👩🎨 Mary's withdrawal scenario above.

In this example, this reward APR% for Bob and Roger is very high, much more than they would have received for other staking methods, as they capture value from STAKE placed in the Easy Staking contract. Distribution percentages will vary based on how much ETH and STAKE exist in liquidity pools and how much STAKE is placed in the Easy Staking contract.

## How to Participate <a id="how-to-participate"></a>

