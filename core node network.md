# Core Node Network

The **core node network** is the foundational peer-to-peer (P2P) system responsible for maintaining and [[propagating]] the global state of the blockchain. It is composed of interconnected computer systems running blockchain node software, including [[SV Node]] and transitioning towards a [[TeraNode]]-dominated topology.

---

## Topology of the Core Node Network

The core node network operates as a **near-complete ultra small-world mandala network**. Each node establishes dedicated connections to peers, ensuring rapid propagation and execution of the six steps defined in **Section 5** of the [[Bitcoin Whitepaper|whitepaper]]:

1. Receiving transactions.
2. Validating transactions against consensus rules.
3. Propagating transactions to peers.
4. Receiving blocks.
5. Validating blocks.
6. Propagating blocks to peers.

The network's design emphasizes efficiency and low latency to maintain the integrity and consistency of the blockchain as the **global timestamp server**.

---

## Responsibilities of the Core Node Network

### Timestamp Server
Nodes collectively maintain the **global record of timestamps** by propagating and validating blocks, ensuring the immutability and chronological ordering of transactions.

### Write Operations
The primary function of the core node network is **write operations** to the **[[WORM Database (Write Once, Read Many)|WORM database]]**, where transaction data and block metadata are permanently stored. These operations form the backbone of the blockchain's integrity.

### [[Overlay Service]] and [[Simplified Payment Verification]]
Overlay services interface with the core node network, handling:

- **Transaction broadcasting**: Businesses broadcast their transactions to the network.
- **UTXO lookups**: Dedicated services maintain [[Simplified Payment Verification]] proofs for [[UTXO|unspent transaction outputs]] related to their specific operations.
- **Block Header Service**: Ensures integrity by providing validated [[Merkle paths]] to overlay services.

Businesses use the overlay layer to segregate concerns, focusing only on UTXOs relevant to their operations. Each business in the **overlay ring** interacts with the core network solely within the bounds of their prescribed activities, maintaining isolation and focus.

---

## Advanced Connectivity and Scalability

### IPv6 and Multicast
To support ultra-connectivity, the core node network increasingly leverages **IPv6 technologies** such as [[multicast]] for efficient data transmission. This is crucial for:

- **Data deduplication**: Reduces redundant transmission when broadcasting transaction or block data to multiple peers.
- **Intrablock [[Subtree]] Streaming**: Nodes can stream intrablock subtrees to peers, ensuring that when a winning block is published, only the most recent subtrees need to be synchronized for block validation.

### Block Validation and Synchronization
- Nodes validate blocks by cross-referencing intrablock subtrees, drastically reducing synchronization time.
- Subtree streaming ensures that nodes are near-instantaneously ready to [[validate]] and propagate a found block.

---

## Tags

#CoreNodeNetwork #P2P #WORMDatabase #SPV #IPv6 #OverlayServices #UTXO #TeraNode #MandalaNetwork #Blockchain #Networking

---

## See Also

- [[Bitcoin Whitepaper]]
- [[TeraNode]]
- [[SV Node]]
- [[UTXO]]
- [[WORM Database (Write Once, Read Many)]]
- [[Block Header Service]]
- [[SPV (Simplified Payment Verification)]]
- [[IPv6 Networking]]
- [[Overlay Service]]
