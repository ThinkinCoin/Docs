# POSDAO Staking Roadmap

The xDai Chain is transitioning to POSDAO, a Proof of Stake consensus protocol. POSDAO will introduce a staking token called STAKE. Individuals who own STAKE may become validators or may delegate their stake to validator candidates to secure the xDai chain. Validators and delegators \(stakers\) will receive rewards in exchange for providing STAKE.

The transition to POSDAO will proceed in phases. Phase 1 of this transition was completed on **April 1, 2020**. Below are details related to the transition & what to expect in each phase.

## ​✅ Phase 1: Preparation and Permissioned POSDAO <a id="phase-1-preparation-and-permissioned-posdao"></a>

Phase 1 was successfully activated April 1, 2020.

POSDAO will launch on the xDai chain with the [current xDai validators](https://validators.poa.network/). **Public validators and delegators will be incorporated in phase 2.**

### Phase 1 STAKE Info <a id="phase-1-stake-info"></a>

* Current validators each receive 20,000 STAKE at the start of the protocol. To participate, the entire amount must be staked.
* Initial validators will receive 15% APR in STAKE rewards \(eg 20k STAKE in protocol =~ 250 STAKE / Mo\) . This rate is subject to adjustment in phase 2.
* STAKE will be compartmentalized within the xDai chain. It cannot be moved to the Ethereum mainnet until phase 2.

### Timeline <a id="timeline"></a>

### Details <a id="details"></a>

In preparation for POSDAO migration, we will complete all required changes to the [Open Ethereum client](https://github.com/poanetwork/open-ethereum) and xDai bridge, and complete all necessary testing. We will provide current validators with detailed upgrade instructions and 20,000 STAKE tokens \(the minimum required amount to become a validator\). **In order to participate, validators must upgrade their nodes by March 31**.

POSDAO v1 is scheduled to go live with current validators on April 1. Public staking will not be activated in phase 1.

POSDAO includes a multi-reward structure for stakers. In addition to STAKE rewards, stakers receive additional xDai rewards. To create these rewards, Dai locked in the bridge contract is converted to [Chai](https://chai.money/about.html), an interest earning form of Dai. The interest accumulated from the locked Chai during a staking epoch is divided amongst stakers at the end of each epoch. In phase 1, we will enable Chai conversion on the xDai bridge. **However, xDai reward dividends will be not be incorporated until phase 2.** [More info on Chai is available here.](https://www.xdaichain.com/for-stakers/stake-token/stake-reward-mechanics/xdai-rewards/chai-faqs)​

## Phase 2: Easy Staking, Public Staking & Reward Expansion <a id="phase-2-easy-staking-public-staking-and-reward-expansion"></a>

After the STAKE public listing is complete and POSDAO is running as expected with the current validator set, staking on xDai will start with EasyStaking and then open up to all public STAKE holders.

### ​✅ EasyStaking on Ethereum <a id="easystaking-on-ethereum"></a>

EasyStaking is now live at: [https://easy-staking.xdaichain.com/](https://easy-staking.xdaichain.com/) EasyStaking Contract: [https://etherscan.io/address/0xecbcd6d7264e3c9eac24c7130ed3cd2b38f5a7ad](https://etherscan.io/address/0xecbcd6d7264e3c9eac24c7130ed3cd2b38f5a7ad)​

The EasyStaking application will be deployed to the Ethereum Mainnet, and will allow participants with any amount of STAKE to participate. Users can commit STAKE to the protocol, and it will earn additional STAKE based on how long it is placed in the application as well as the total amount staked by all participants. For more details, see the [EasyStaking page](easystaking-on-ethereum.md).

* Minimum &lt;.0001 STAKE, no Maximum
* Rewards based on time and total amount staked
* **POSDAO Staking on xDai**
* Minimums may be changed with a governance proposal. Initial staking requirements:
  * Validator Candidate: 20,000 STAKE Minimum
  * Delegator: 200 STAKE Minimum
* STAKE reward % will vary based on role \(validator or delegator\) and amount of total STAKE locked in the protocol. The APR may be adjusted from phase 1 \(15%\). For more details, see the [reward distribution section of the POSDAO whitepaper](https://forum.poa.network/t/posdao-white-paper/2208).
* The STAKE bridge will open bi-directionally, allowing STAKE to flow freely from the Ethereum mainnet to the xDai chain and back.

### Processes <a id="processes"></a>

### Public Staking Details <a id="public-staking-details"></a>

Public participation will open in phase 2. Individuals can acquire STAKE on the mainnet \([how to get STAKE](https://www.xdaichain.com/for-stakers/stake-token/get-stake)\) and

1. Immediately stake it into the EasyStaking application \(see [EasyStaking](easystaking-on-ethereum.md) for more info\)
2. Bridge it to the xDai chain. Here, it can be used in the protocol to secure the chain and earn staking rewards. STAKE actions on xDai are intuitive and easy to perform through the staking UI.

**POSDAO Staking on xDai**

Individuals with the minimum required STAKE and the ability to run a node may register as validator candidates. STAKE can also be delegated on validator candidates, forming a pool. Candidate pools with the most STAKE will have the greatest chance of selection to the next validator set \(if there are more than 19 validator pools. If 19 or less all candidates become validators\).

Validator sets will update after each staking epoch, initially set at 1 week intervals.

With public participation, additional rewards may be added to the protocol.

1. A fee will be charged when xDai is converted to Dai through the xDai bridge \(moved from the xDai chain to the Ethereum mainnet\). This fee \(% TBD\) will be distributed to validator pools active when the conversion occurs.
2. Interest earned from Chai locked in the bridge will be distributed as xDai to active validator pools. Additional Dai may be added to the bridge and converted to Chai to increase the interest reward at the team's discretion. _\(this features is on indefinite hold due to the 0 Dai Savings Rate\)_

## Phase 3: HoneyBadger BFT Consensus Layer Integration <a id="phase-3-honeybadger-bft-consensus-layer-integration"></a>

No timeline is set yet for HBBFT integration, we will provide further details once phase 2 is complete. [More information on HBBFT is available here.](https://www.xdaichain.com/for-validators/consensus/honeybadger-bft-consensus)​

