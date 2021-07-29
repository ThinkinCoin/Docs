# On-Chain Random Numbers

The xDai stable chain features an on-chain RNG based on RANDAO. It may be leveraged by smart contract developers to introduce random numbers into their applications. _Note that random numbers are limited to certain blocks in the current implementation. See below for more information._

## Randomness Contract \(RandomAuRa\) <a id="randomness-contract-randomaura"></a>

RandomAura is an upgradeable contract, so it includes both an implementation and proxy address. To access, utilize the proxy address \(`RandomAuraProxy`\) along with the ABI of the implementation contract \(`RandomAuraCode`\). Seed values are read from the proxy contract.

The current implementation requires a chain running Parity's AuRa consensus mechanism with version 3.2.5+ or Nethermind v 1.10.71. The Random Number generation contract was [introduced in this PR](https://github.com/paritytech/parity-ethereum/pull/10946).

