# Lachesis aBFT

Lachesis is a break-through **aBFT consensus algorithm** developed by Fantom.

Below are the key properties of Lachesis algorithm:

* **Asynchronous**: Participants have the freedom to process commands at different times.
* **Leaderless**: No participant plays a “special” role.
* **Byzantine Fault-Tolerant**: Functional in a presence of up to one-third of faulty nodes and

  malicious nodes.

* **Final**: Lachesis's output can be used immediately. Transactions are confirmed within 1-2 seconds.

The platform is **modular** and **compatible** with other dev tools such as the EVM or the Cosmos SDK. It can easily be **integrated into any blockchain**.

Lachesis allows to scale transaction throughput while keeping **instant finality** and without an increased risk of centralization.

## How does Lachesis work? <a id="how-does-lachesis-work"></a>

Each Lachesis node stores a local **Acyclic Directed Graph \(DAG\)** composed of event blocks, each of which consists of transactions. The DAG, capturing the happens-before relationship between the events, is used to calculate an exact final order of events—and hence transactions—independently on each node.

Event blocks are either confirmed or unconfirmed event blocks. New event blocks are unconfirmed, whereas **event blocks from the past 2-3+ frames are all confirmed**, and subsequently ordered by honest nodes.

Consensus results in batches of confirmed event blocks, where each batch of events is called a block. **Finalized blocks forming the final chain** are calculated independently from the local DAG of event blocks stored on each node.

Unlike Proof-of-Work, round-robin Proof-of-Stake, coinage Proof-of-Stake, and sync BFT, Lachesis **nodes do not send blocks to each other. Only the events are being synced between nodes**. Validators don’t vote on a concrete state of the network; instead, they periodically exchange observed transactions and events with peers.

Unlike Classical consensus, such as pBFT, Lachesis does not use new events in the current election; but instead, new events are used to vote for the events in 2-3+ previous virtual elections simultaneously. This leads to a **smaller number of created consensus messages**, as the same event is reused in different elections. Hence, Lachesis achieves a **lower time to finality and a smaller communication overhead** compared to synchronous BFT.

### What are epochs in Lachesis? <a id="what-are-epochs-in-lachesis"></a>

Lachesis’s event structure is a DAG of events. To optimize storage and retrieval, the DAG is separated into sub-DAGs, each of them is called an epoch. Each epoch comprises many finalized blocks.

Each epoch is sealed when one of these conditions is satisfied:

* The epoch reaches a defined number of blocks
* The epoch lasts for a specified time
* At least one cheater is found in this block

When an epoch gets sealed, its inner epoch indexes get pruned, and new events of the sealed epochs are ignored. Each epoch forms a separate DAG, and thus parents from other epochs are not allowed.

For a sanity check, each event includes the hash of the previous epoch.

## Comparison of Consensus Protocols <a id="comparison-of-consensus-protocols"></a>

