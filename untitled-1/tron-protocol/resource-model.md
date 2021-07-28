# Resource Model

## Introduction <a id="introduction"></a>

TRON network has four types of resources: Bandwidth, CPU, Storage and RAM. Benefit by TRON's exclusive RAM model, TRON's RAM resource is almost infinite.

TRON network imports two resource conceptions: Bandwidth points and Energy. Bandwidth Point represents Bandwidth; Energy represents CPU and Storage.

**Note:**

* Ordinary transaction only consumes Bandwidth points
* Smart contract related transaction consumes not only Bandwidth points, but also Energy

## Bandwidth Points <a id="bandwidth-points"></a>

The transaction information is stored and transmitted in the form of the byte array; Bandwidth Points consumed = the number of bytes of the transaction \* Bandwidth Points rate. Currently Bandwidth Points rate = 1

Such as if the number of bytes of a transaction is 200, so this transaction consumes 200 Bandwidth Points.

**Note:** Due to the change of the total amount of the frozen TRX in the network and the self-frozen TRX amount, the Bandwidth Points an account possesses is not fixed.

### 1. How to Get Bandwidth Points <a id="1-how-to-get-bandwidth-points"></a>

* By Freezing TRX to get Bandwidth Points, Bandwidth Points = the amount of TRX self-frozen / the total amount of TRX frozen for Bandwidth Points in the network \* 43\_200\_000\_000
* Every account has a fixed amount of free Bandwidth Points\(5000\) every day

### 2.Bandwith Points Consumption <a id="2-bandwith-points-consumption"></a>

Except for query operation, any transaction consumes Bandwidth points.

There's another situation: When you transfer\(TRX or token\) to an account that does not exist in the network, this operation will first create that account in the network and then do the transfer. It only consumes Bandwidth points for account creation, and no extra Bandwidth points consumption for transfer.

Create a new account transaction, Bandwidth points consumption sequence: 1.Bandwidth points from freezing TRX. If transaction initiator does not have enough Bandwidth Points of this type, it will go to step 2;

1. Burn 0.1 TRX;

Token transfer transaction, Bandwidth points consumption sequence:

1. Firstly, check if the total free Bandwidth Points of the token issuer is enough. Then, check if the transfer Initiator‘s remaining token free bandwidth Points is enough. Finally check if the Bandwidth Points of token issuer obtained by freezing TRX is enough. Otherwise, it will go to step 2; 2.Bandwidth points from freezing TRX. If transaction initiator does not have enough Bandwidth Points of this type, it will go to step 3; 3.Free Bandwidth points. If transaction initiator does not have enough Bandwidth Points of this type, it will go to step 4; 4.Bandwidth points from burning TRX, the rate = the number of bytes of the transaction \* 140 SUN;

The ordinary transaction, Bandwidth points consumption sequence: 1.Bandwidth points from freezing TRX. If transaction initiator does not have enough Bandwidth Points of this type, it will go to step 2;

2.Free Bandwidth points. If transaction initiator does not have enough Bandwidth Points of this type, it will go to step 3;

3.Bandwidth points from burning TRX, the rate = the number of bytes of the transaction \* 140 SUN;

### 3. Bandwidth Points Recovery <a id="3-bandwidth-points-recovery"></a>

Every 24 hours, the amount of the usage of Bandwidth points of an account will be reset to 0. For the specific formula:![](https://files.readme.io/15610eb-WechatIMG250.png)​![](https://files.readme.io/15610eb-WechatIMG250.png)​

Bandwidth recovery formula

Every 24 hours, the amount of the usage of Bandwidth points of an account will be reset to 0.

## Energy <a id="energy"></a>

Each command of smart contract consume system resource while running, we use 'Energy' as the unit of the consumption of the resource.

### 1. How to Get Energy <a id="1-how-to-get-energy"></a>

Freeze TRX to get energy.

**Example \(Using wallet-cli\):**Shell

```text
freezeBalance frozen_balance frozen_duration [ResourceCode:0 BANDWIDTH,1 ENERGY]
```

Freeze TRX to get energy, energy obtained = user's TRX frozen amount / total amount of frozen TRX in TRON \* 90\_000\_000\_000.

Example:Java

```text
If there are only two users, A freezes 2 TRX, B freezes 2 TRXthe energy they can get is:A: 45_000_000_000 and energy_limit is 45_000_000_000B: 45_000_000_000 and energy_limit is 45_000_000_000​when C freezes 1 TRX:the energy they can get is:A: 36_000_000_000 and energy_limit is 36_000_000_000B: 36_000_000_000 and energy_limit is 36_000_000_000B: 18_000_000_000 and energy_limit is 18_000_000_000
```

**Energy Recovery** The energy consumed will reduce to 0 smoothly within 24 hours.

Example:Java

```text
at one moment, A has used 72_000_000 Energyif there is no continuous consumption or TRX freezeone hour later, the energy consumption amount will be 72_000_000 - (72_000_000 * (60*60/60*60*24)) Energy = 69_000_000 Energy24 hours later, the energy consumption amount will be 0 Energy
```

### 2. How to Set Fee Limit \(Caller Must Read\) <a id="2-how-to-set-fee-limit-caller-must-read"></a>

Within the scope of this section, the smart contract developer will be called "developer", the users or other contracts which call the smart contract will be called "caller"

The amount of energy consumed while call the contract can be converted to TRX or SUN, so within the scope of this section, when refer to the consumption of the resource, there's no strict difference between Energy, TRX and SUN, unless they are used as a number unit.

Set a rational fee limit can guarantee the smart contract execution. And if the execution of the contract cost great energy, it will not consume too much energy from the caller. Before you set fee limit, you need to know several conception:

1.The legal fee limit is a integer between 0 - 5\*10^9, unit is SUN.

2.Different smart contracts consume different amount of energy due to their complexity. The same trigger in the same contract almost consumes the same amount fo energy\[1\]. When the contract is triggered, the commands will be excuted one by one and consume energy. If it reaches the fee limit, commands will fail to be excuted, and energy is not refundable.

3.Currently fee limit only refers to the energy converted to SUN that will be consumed from the caller. The energy consumed by triggering contract also includes developer's share.

4.For a vicious contract, if it encounters execution timeout or bug crash, all it's energy will be consumed.

5.Developer may undertake a proportion of energy consumption\(like 90%\). But if the developer's energy is not enough for consumption, the rest of the energy consumption will be undertaken by caller completely. Within the fee limit range, if the caller does not have enough energy, then it will burn equivalent amount of TRX.

To encourage caller to trigger the contract, usually developer has enough energy.

### 3. Energy Calculation \(Developer Must Read\) <a id="3-energy-calculation-developer-must-read"></a>

1.In order to punish the vicious developer, for the abnormal contract, if the execution times out \(more than 80ms\) or quits due to bug \(revert not included\), the maximum available energy will be deducted. If the contract runs normally or revert, only the energy needed for the execution of the commands will be deducted.

2.Developer can set the proportion of the energy consumption it undertakes during the execution, this proportion cna be changed later. If the developer's energy is not enough, it will consume the caller's energy.

3.Currently, the total energy available when trigger a contract is composed of caller fee limit and developer's share

**Note:**

* If the developer is not sure about whether the contract is normal, do not set caller's energy consumption proportion to 0%, in case all developer's energy will be deducted due to vicious execution.
* We recommend to set caller's energy consumption proportion to 10% ~ 100%.

If contract executes successfully without any exception, the energy needed for the execution will be deducted. Generally, it is far more less than the amount of energy this trigger can use.

If Assert-style error come out, it will consume the whole number of energy set for fee limit.

Assert-style error introduction, refer to：[Exception Handling](https://developers.tron.network/docs/exception-handling)​

To avoid unnecessary lost, 10 - 100 is recommended for consume\_user\_resource\_percent.

## Resource Delegation <a id="resource-delegation"></a>

In TRON network, an account can freeze TRX for Bandwidth or Energy for other accounts. The primary account owns the frozen TRX and TRON power, the recipient account owns the Bandwidth or Energy. Like ordinary freezing, resource delegation freezing is also at least 3 days.Java

```text
freezeBalance frozen_balance frozen_duration [ResourceCode:0 BANDWIDTH,1 ENERGY] [receiverAddress]​frozen_balance: the amount of TRX to freeze (unit SUN)  frozen_duration: the freezing period (currently a fixed 3 days)ResourceCode: 0 for Bandwidth, 1 for Energy  receiverAddress: recipient account address
```

