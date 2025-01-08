
**`OP_RETURN`** is an opcode in [[Bitcoin Script]] that is often used for embedding non-spendable data within the ledger. Originally designed to mark outputs as provably unspendable, `OP_RETURN` has evolved in its usage and size constraints over the years, and it plays a key role in applications like logging, timestamping, and [[Digital Asset Recovery]].

---

## History of OP_RETURN

### Initial Purpose

`OP_RETURN` was introduced to enable transaction outputs to be marked as unspendable, reducing [[UTXO]] bloat. The opcode effectively allows embedding metadata into a transaction while ensuring that the output cannot be redeemed.

### The OP_RETURN Bug

In the early implementation of `OP_RETURN`, a critical bug allowed outputs marked with `OP_RETURN` to be mistakenly spendable under certain circumstances. This led to confusion over its correct usage, which was later rectified to strictly enforce its non-spendable nature.

### Size Restrictions Over Time

1. **Reduction in Payload Size**:  
   In Bitcoin Core (BTC), the size of `OP_RETURN` payloads was significantly reduced to 80 bytes as part of efforts to limit "non-financial" transactions and reduce blockchain bloat. This restriction curtailed many creative uses of the opcode.  

2. **Post-Split Evolution**:  
   After the [[BSV Blockchain]] and BCH split, BSV removed these restrictions, allowing for much larger `OP_RETURN` payloads. This opened the door for embedding larger data sets directly onto the blockchain, although this usage is often debated.

---

## Current Usage of OP_RETURN

### Data Payloads and Timestamping

- **Data Embedding**:  
  Many use `OP_RETURN` to embed metadata, including text, hashes, and small files, directly into the blockchain for purposes like [[censorship resistance]]. While functional, embedding large data payloads is not considered the most efficient use of the opcode.

- **Optimal Usage**:  
  The best use of `OP_RETURN` is as a **carriage return** or **print function**, logging a statement on the blockchain rather than embedding large payloads. For example:
  - Embedding **hashes** of documents or datasets for [[Timestamping|timestamping]] purposes.  
  - Providing references to off-chain data, ensuring its integrity via the blockchain.

### Non-Spendable Outputs

Outputs marked with `OP_RETURN` are provably unspendable, meaning they do not increase the [[UTXO set]]. This reduces the burden on the network, making it a cleaner option for logging information compared to creating spendable outputs.

---

## Role in [[Digital Asset Recovery]] (DAR)

### Modified Use of OP_RETURN

In the context of DAR, `OP_RETURN` can be leveraged for reassigning digital assets under court order without rewriting the ledger:

1. **Modified Script**:  
   Normally, `OP_RETURN` outputs are prefixed with `OP_FALSE` to ensure their validity as unspendable. For DAR purposes, this prefix can be omitted, allowing the output to direct funds to a new [[UTXO]].

2. **Process**:  
   - The transaction includes an `OP_RETURN` output referencing the court order and the new UTXO for the reassigned funds.  
   - Miners are notified via the [[Alert System]] to process this transaction.  
   - Miners are obligated to validate and accept these transactions to remain compliant with the [[Network Access Rules]].

3. **Key Benefits**:  
   - Ensures that asset recovery is traceable through the blockchain.  
   - Avoids rewriting historical transactions.  
   - Logs the legal basis for the reassignment directly on the ledger.

---

## Tags

- [[OP_RETURN]]  
- [[Bitcoin Script]]  
- [[Timestamping]]  
- [[Digital Asset Recovery]]  
- [[Blockchain Logging]]  
- [[Network Access Rules]]  
- [[UTXO]]  
- [[Data Embedding]]  
