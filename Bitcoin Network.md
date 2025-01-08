## Overview

The **Bitcoin Network** is a system of interconnected nodes that implement the [[Bitcoin Protocol]]. These nodes, referred to as **miners**, are responsible for constructing, validating, and distributing blocks across the network. The Bitcoin network is defined in [[Satoshi Nakamoto's Whitepaper]], specifically in Section 5, and operates as a [[Peer-to-Peer (P2P) Network]] without any hierarchy in block distribution or validation.

While multiple implementations of the Bitcoin Protocol exist (e.g., [[BTC]], [[BCH]], and [[BSV Blockchain]]), they have diverged significantly in terms of consensus rules, data structures, and signature schemes. Among these, the [[BSV Network]] is regarded as the legitimate Bitcoin Network by adhering to the original protocol and principles outlined in the whitepaper.

---

## Characteristics of the Bitcoin Network

### 1. **Nodes as the Foundation**
- A **node** is defined as an entity capable of:
  - Constructing valid blocks.
  - Distributing blocks to peers.
  - Validating blocks and transactions.
- There is no distinction between "archival" or "propagation" nodes on the network.
- Nodes are incentivized to maintain high connectivity, resulting in a near-complete graph topology.

### 2. **Decentralized, Peer-to-Peer Structure**
- The network is truly [[decentralized]] and [[P2P]]:
  - Blocks are propagated directly between nodes without intermediaries.
  - Nodes join and leave the network dynamically.
- At any given time, a small number of nodes produce the majority of blocks.

### 3. **User Interaction**
- Users are external to the Bitcoin Network and interact with nodes via client software.
- Users can take various forms, including:
  - Wallets.
  - Service providers.
  - Storage entities.
  - Autonomous agents (e.g., [[Smart Contract]]).
- Users are not part of the consensus process and do not validate or propagate blocks.

### 4. **Layered User Networks**
- User networks may exist as overlays on top of the Bitcoin Network:
  - These networks can be [[P2P]] or hierarchical.
  - Examples include service-provider-consumer relationships and [[Overlay Service]].
- Such networks enhance functionality while remaining distinct from the core Bitcoin Network.

---

## Bitcoin Network Variants

### 1. **BTC (Bitcoin Core)**
- Deviated from the original protocol by introducing [[SegWit]] and [[Taproot]], altering data structures and consensus rules.
- Relies on second-layer solutions like the [[Lightning Network]] to address scalability limitations.
- Operates under hard-capped block sizes, creating high transaction fees and delays.

### 2. **BCH (Bitcoin Cash)**
- Introduced [[Canonical Transaction Ordering (CTOR)]] and expanded block sizes.
- Focuses on on-chain scalability but lacks certain scripting capabilities restored in BSV.

### 3. **BSV (Bitcoin Satoshi Vision)**
- Restores and locks the original Bitcoin Protocol.
- Offers unbounded scalability and supports advanced applications such as [[Overlay Service]], [[IoT]], and [[Smart Contract]].
- Enforces the original [[Chain of Digital Signatures]], maintaining compatibility with [[Simplified Payment Verification (SPV)]].

---

## Nodes and Consensus

### 1. **Role of Nodes**
- Nodes uphold the network's consensus mechanism based on [[Proof of Work]] (PoW).
- They validate blocks and transactions according to the network's rules, ensuring security and reliability.

### 2. **Consensus Variations**
- Each network (BTC, BCH, BSV) enforces unique consensus rules, resulting in protocol incompatibilities:
  - [[Data Structures]] like blocks and transactions vary.
  - Signature schemes differ, affecting how transactions are validated.

### 3. **BSV as the Legitimate Bitcoin Network**
- BSV retains the original protocol's rules, data structures, and signature schemes.
- It supports enterprise-grade scalability and aligns with the vision outlined in the Bitcoin Whitepaper.

---

## Bitcoin Network Functionality

### 1. **Block Construction and Validation**
- Blocks link to previous blocks using cryptographic hashes, forming a secure chain.
- Nodes ensure that blocks meet network rules, such as correct [[Proof of Work]] and valid transactions.

### 2. **Transaction Propagation**
- Transactions enter the network via users interacting with nodes.
- Nodes validate and propagate transactions across the network, ensuring they comply with protocol rules.

### 3. **Scalability and Overlays**
- The BSV Network supports large-scale applications through [[Overlay Service]] and unbounded block sizes.
- Overlays enable advanced functionality, such as [[IoT]] integrations, without altering the core protocol.

---

## Challenges and Contentions

### 1. **Protocol Divergence**
- The split into BTC, BCH, and BSV has created debate over which network represents "Bitcoin."
- BTC's and BCH's deviations from the original protocol have led to criticisms of mutability and reduced functionality.

### 2. **Economic Incentives**
- Each network's economic model influences miner behavior and network priorities.

### 3. **Legitimacy**
- BSV proponents argue that BTC and BCH have mutated the protocol, while BSV adheres to the original vision.

---

## Tags

#BitcoinNetwork #BitcoinProtocol #BSV #BTC #BCH #P2P #Blockchain #ConsensusRules #Nodes #Scalability #OverlayServices #SmartContracts #BitcoinWhitepaper #ProofOfWork

---

## See Also

- [[Bitcoin Protocol]]
- [[Consensus Rules]]
- [[Digital Signatures]]
- [[Simplified Payment Verification (SPV)]]
- [[Blockchain]]
- [[Proof of Work]]
- [[Overlay Service]]
- [[Smart Contract]]


