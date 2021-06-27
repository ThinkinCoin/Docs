# Transaction Fees

## Basics <a id="basics"></a>

Each transaction on Fantom requires a transaction fee paid to the network in order to prevent spam attacks. The fee is paid in FTM \(Fantom's native token\).

Transactions fees are paid to validators to reward them for processing transactions.

## Rewards distribution <a id="rewards-distribution"></a>

Rewards distribution is fully controlled by an SFC contract. The SFC contract can be upgraded by governance at any time without hardfork.

30% of transaction fees are held by the SFC contract \(those funds aren't used\). The remaining 70% of transaction fees are distributed between validators proportional to their `transactions reward weight`.

To learn more about the validator economy employed on Fantom, please refer to our [Github](https://github.com/Fantom-foundation/go-lachesis/wiki/Validator----Economy).

