The **Bitcoin Protocol** is a fixed set of data structures, file formats, and consensus rules that define the behavior of nodes participating in the [[Bitcoin]] network. It is the foundation of the [[BSV Blockchain]] blockchain, establishing how transactions, blocks, and network communication occur. The protocol is intentionally **set in stone**, ensuring stability and interoperability while providing a decentralised governance model.

---

## Defining the Bitcoin Protocol

### 1. **Core Components of the Protocol**
The Bitcoin Protocol encompasses:
- **Data Structures**:
  - [[Transactions]]: Defined by input and output structures such as [[scriptPubKey]], [[scriptSig]], and [[TXID]].
  - [[Blocks]]: Comprised of a block header, [[Merkle Root]], and a batch of transactions.
- **Consensus Rules**:
  - Defines how nodes validate transactions and blocks.
  - Enforces the [[Chain of Digital Signatures]] and prevents [[Double-Spending]].
- **File Formats**:
  - Specifies how data is stored and transmitted across the network.
  - Includes standardization of [[UTXO]] records and network messages.
- **[[Network Access Rules (NAR)]]**:
  - Defines the conditions under which nodes can participate in the network.
  - Ensures adherence to consensus rules and filters malicious actors.

### 2. **Set in Stone**
The protocol is designed to be immutable:
- **[[Decentralisation]]**:
  - Ensures no single entity or group can unilaterally alter the rules or data structures.
  - Stability allows businesses and applications to rely on the protocol without fear of disruptive changes.
- **Honest Nodes**:
  - An honest node follows all consensus rules as outlined in the [[Bitcoin Whitepaper]] and commits to maintaining the longest honest chain.

### 3. **Mutable Components**
While the core protocol is immutable, certain non-consensus-critical components may evolve:
- **[[Hash Functions]]**:
  - If a hash function (e.g., SHA-256) becomes insecure, it can be replaced through a carefully coordinated upgrade process.
- **Networking Optimizations**:
  - Improvements to communication protocols and efficiency do not affect consensus.
- **[[Overlay Service]]**:
  - Application-specific layers (e.g., identity management or [[Digital Asset Recovery]]) can be built atop the protocol.

---

## Consensus Rules

### Definition
Consensus rules ensure that all nodes validate transactions and blocks consistently. Key rules include:
1. **Double-Spending Prevention**:
   - Transactions must reference unspent [[UTXO]]s.
2. **Block Validity**:
   - Blocks must have a valid [[Merkle Root]], correct [[Proof of Work]], and follow size limits.
3. **Transaction Scripts**:
   - [[scriptPubKey]] and [[scriptSig]] must resolve to `TRUE` to unlock and spend outputs.

### Honest Nodes
An honest node:
- Follows all protocol rules without deviation.
- Propagates valid blocks and transactions.
- Builds on the **longest [[honest chain]]** by contributing valid [[Proof of Work]].

### Network Access Rules (NAR)
The [[Network Access Rules]] define the protocol's boundary:
- Nodes must validate all incoming data against consensus rules.
- Transactions violating rules (e.g., malformed scripts) are rejected.
- Helps prevent malicious activity and maintain protocol integrity.

---

## Key Features of the Bitcoin Protocol

### 1. **Fixed Data Structures**
- Transactions and blocks are immutable in format, enabling compatibility across implementations.
- Ensures that applications built today will work seamlessly in the future.

### 2. **Consensus-Based Decentralisation**
- Rules are enforced by network participants rather than a central authority.
- Any node attempting to deviate is excluded from the honest network.

### 3. **Interoperability**
- Fixed structures allow multiple implementations to coexist while adhering to the same rules.
- Examples include [[BSV Blockchain]], BTC, and BCH, though only BSV maintains the original protocol's design and intent.

---

## Challenges in Protocol Deviations

### 1. **BTC (Bitcoin Core)**
- Frequent changes to consensus rules and data structures (e.g., SegWit, Taproot).
- Introduces centralisation as decisions are made by a small group of developers.
- Protocol mutability undermines long-term stability and trust.

### 2. **BCH (Bitcoin Cash)**
- Increased block size but failure to restore full functionality (e.g., limited [[Bitcoin Script]]).
- Lacks the unbounded scalability of [[BSV Blockchain]].

### 3. **BSV**
- Restores and locks the original Bitcoin protocol as outlined in the whitepaper.
- Provides stability and scalability, adhering to the principle of being set in stone.

---

## Advantages of a Fixed Protocol

### 1. **Stability**
- Developers and businesses can plan projects without fear of disruptive changes.

### 2. **Decentralisation**
- No single group can unilaterally alter the protocol, ensuring governance aligns with network participants' interests.

### 3. **Interoperability**
- Ensures consistent functionality across all compliant nodes.

### 4. **Trust**
- Participants have confidence in the protocol's predictability and reliability.

---

## Tags

#BitcoinProtocol #ConsensusRules #SetInStone #NetworkAccessRules #BSV #Decentralisation #Blockchain #ImmutableRules

---

## See Also

- [[Bitcoin]]
- [[Consensus Rules]]
- [[Network Access Rules (NAR)]]
- [[Bitcoin Whitepaper]]
- [[Chain of Digital Signatures]]
- [[Proof of Work]]
- [[Digital Asset Recovery]]
- [[Bitcoin Script]]
- [[UTXO Model]]
