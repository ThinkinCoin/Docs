# Technology

## Foundation for the Internet of Value and People <a href="#headline-5-10" id="headline-5-10"></a>

Polygon provides the core components and tools to join the new, borderless economy and society

![](https://polygon.technology/wp-content/uploads/2021/02/Foundation-of-the-Internet-Diagram.png)

With polygon, any project can easily spin-up a dedicated blockchain network which combines the best features of stand-alone blockchains (sovereignty, scalability and flexibility) and Ethereum (security, interoperability and developer experience). Additionally, these blockchains are compatible with all the existing Ethereum tools (Metamask, MyCrypto, Remix etc), and can exchange messages among themselves and with Ethereum.

Polygon technology is materialized through two major components: Polygon framework and Polygon protocol.

## Framework <a href="#headline-18-10" id="headline-18-10"></a>

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

One-click deployment of preset Ethereum-compatible blockchains

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Growing set of modules (pluggable consensus, staking, governance, EVM/Ewasm, execution environments, dispute resolvers etc.) for developers who want to build their custom blockchains

## Protocol <a href="#headline-29-10" id="headline-29-10"></a>

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Arbitrary message passing between any two participating Polygon chains, as well as between any Polygon chain and Ethereum

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

"Security as a service" (non-mandatory, modular security services, provided either by Ethereum directly or by a dedicated set of validators)

## Polygon Chains <a href="#headline-42-10" id="headline-42-10"></a>

Polygon supports two major types of Ethereum-compatible blockchain networks: stand-alone networks and networks that leverage “security as a service”

![](https://polygon.technology/wp-content/uploads/2021/02/polygon-chains.png)

### Secured Chains <a href="#headline-50-10" id="headline-50-10"></a>

Blockchain networks that use “security as a service” instead of establishing their own validator pool. The service can be provided either by Ethereum directly (via fraud proofs or validity proofs) or by a pool of professional validators (similar to Polkadot’s “shared security”). Secured chains offer high level of security, with the tradeoff of sacrificing a portion of independence and flexibility.

#### Implementations <a href="#headline-54-10" id="headline-54-10"></a>

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

zk Rollups

![](https://polygon.technology/wp-content/uploads/2021/02/coming-soon.png)

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Optimistic Rollups

![](https://polygon.technology/wp-content/uploads/2021/02/coming-soon.png)

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Validum Chains

![](https://polygon.technology/wp-content/uploads/2021/02/coming-soon.png)

### Stand-alone Chains <a href="#headline-82-10" id="headline-82-10"></a>

Fully sovereign Ethereum-compatible blockchain networks. These networks are fully in charge of their own security, i.e. have their own pool of validators. Stand-alone chains offer the highest level of independence and flexibility, with the tradeoff of sometimes challenging validator pool establishing.

#### Implementations <a href="#headline-84-10" id="headline-84-10"></a>

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Sidechains

![](https://polygon.technology/wp-content/uploads/2021/02/coming-soon.png)

![](https://polygon.technology/wp-content/uploads/2021/01/polygon-icon-purple.png)

Enterprise Chains

![](https://polygon.technology/wp-content/uploads/2021/02/coming-soon.png)

![](https://polygon.technology/wp-content/uploads/2021/02/stand-alone-chanes.png)

### Explore Polygon Technology <a href="#headline-102-10" id="headline-102-10"></a>

Or read the whitepaper for a deep dive

## Architecture

Polygon architecture consists of four abstract, composable layers

*

    ![](https://polygon.technology/wp-content/uploads/2021/02/illustrate-architecture.png)
*   **Ethereum layer**

    Polygon chains can use Ethereum, the most secure programmable blockchain in the world, to host and execute any mission-critical component of their logic. This layer is implemented as a set of Ethereum smart contracts, in charge of functions like:

    Finality/checkpointing

    Staking

    Dispute resolving

    Message relaying
*   **Security layer**

    A specialized, non-mandatory layer managing a set of validators that can periodically check the validity of any Polygon chain for a fee. This layer can be implemented as a meta-blockchain that runs in parallel to Ethereum, in charge of functions like:

    Validator management\
    (registration/deregistration, rewards, shuffling etc)

    Polygon chains validation

    Security layer is fully abstract and can have multiple instances, implemented by different entities and with different characteristics. It can also be implemented directly on Ethereum, in which case the Ethereum miners perform the validation.
*   **Polygon networks layer**

    A constellation of sovereign blockchain networks. Each of the networks serves its respective community, maintaining functions like:

    Transaction collation

    Local consensus

    Block production

    The networks can utilize Polygon protocol to connect with each other and exchange arbitrary messages.
*   **Execution layer**

    This layer interprets and executes transactions that are agreed upon and included in Polygon networks’ blockchains. It consists of two sublayers:

    Execution environment\
    (pluggable virtual machine implementation)

    Execution logic\
    (state transition function of a specific Polygon network, normally written as Ethereum smart contracts)

## Positioning <a href="#headline-125-10" id="headline-125-10"></a>

Brief comparison with the most notable alternatives suggests that Polygon offers the most attractive set of features

|                        | Sidechains        | Sharding          | Quorum | Cosmos            | Polkadot          | Polygon |
| ---------------------- | ----------------- | ----------------- | ------ | ----------------- | ----------------- | ------- |
| Ethereum compatibility | ● exclamation-svg | ● exclamation-svg | ●      | ● exclamation-svg |                   | ●       |
| Scalability            | ●                 | ● exclamation-svg | ●      | ●                 | ● exclamation-svg | ●       |
| Security               |                   | ●                 |        |                   | ●                 | ●       |
| Sovereignty            | ●                 |                   | ●      | ●                 | ● exclamation-svg | ●       |
| Interoperability       |                   | ●                 |        | ● exclamation-svg | ●                 | ●       |
| User Experience        | ●                 |                   | ●      | ●                 | ●                 | ●       |
| Developer Experience   |                   | ● exclamation-svg |        |                   |                   | ●       |

|                   | Sidechains        | Sharding          | Quorum | Cosmos            | Polkadot          | Polygon |
| ----------------- | ----------------- | ----------------- | ------ | ----------------- | ----------------- | ------- |
| Eth-compatibility | ● exclamation-svg | ● exclamation-svg | ●      | ● exclamation-svg |                   | ●       |
| Scalability       | ●                 | ● exclamation-svg | ●      | ●                 | ● exclamation-svg | ●       |
| Security          |                   | ●                 |        |                   | ●                 | ●       |
| Sovereignty       | ●                 |                   | ●      | ●                 | ● exclamation-svg | ●       |
| Interoperability  |                   | ●                 |        | ● exclamation-svg | ●                 | ●       |
| User Experience   | ●                 |                   | ●      | ●                 | ●                 | ●       |
| Dev Experience    |                   | ● exclamation-svg |        |                   |                   | ●       |

exclamation-svg

Conditional / Limited

![](https://polygon.technology/wp-content/uploads/2021/02/exclamation-mark.svg)

Conditional / Limited

### Get started with Polygon <a href="#headline-134-10" id="headline-134-10"></a>

Or read the whitepaper to learn more about our technology\
crosschevron-down-circle
