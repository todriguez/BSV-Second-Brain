# VOUT

**VOUT** refers to a **transaction output** in a Bitcoin [[Transaction|transaction]]. It has two distinct interpretations in the technical specification of the [[BSV Blockchain]]:

---

## 1. **VOUT as an Index**
- When used in a **transaction input**, "vout" is a **4-byte index value**.
- This index, combined with the [[TXID]] of the referenced transaction, forms a **transaction outpoint**:
  - **Outpoint:** `TxID || vout`
  - This uniquely identifies a specific output in a previous transaction that is being spent.
- As the index is a 4-byte integer, it supports up to \( 2^{32} \) outputs in a single transaction.

---

## 2. **VOUT as an Output Vector**
- When not used as part of an input, "vout" refers to the **vector of all outputs** in a transaction.
- Each output in the vector contains:
  1. **Value:** The amount of [[Satoshis]] (smallest unit of Bitcoin) being transferred.
  2. **Locking Script (scriptPubKey):** A [[Bitcoin Script]] that defines the conditions required to spend the output.

- The **order of outputs** in the vector matters as it determines the index value of each output.

---

## Unspent Transaction Outputs (UTXOs)
- If an outpoint remains **unspent**, it is referred to as an **Unspent Transaction Output (UTXO)**.
- UTXOs represent the available balance for a wallet or address.
- A UTXO can be used as an input in a new transaction, provided the user satisfies the spending conditions defined by the [[lockScript|locking script]].

- Once a UTXO has been included in a validated transaction, it is considered **spent** and cannot be reused. This mechanism prevents [[Double-spending|double-spending]].

---

## Zero-Value Outputs
1. **Provably Unspendable Outputs:**
   - Zero-value outputs are often used to carry **large data items** or tokens.
   - Outputs with a **false return** script (e.g., OP_FALSE OP_RETURN) attach data to transactions but are not stored in the UTXO set.

2. **Spendable Zero-Value Outputs:**
   - Non-false return zero-value outputs remain valid UTXOs.
   - These outputs can be used as inputs in new transactions, subject to standard [[lockScript|locking conditions]].

---

## VOUT in Bitcoin Transactions
### Example
A transaction output contains:
1. **Value:** 10,000 satoshis.
2. **Locking Script:** 
   ```asm
   OP_DUP OP_HASH160 <PubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
This VOUT specifies that 10,000 satoshis are locked to a public key hash. The recipient must satisfy the conditions in the locking script to unlock the funds.

---

## Use Cases

1. **Standard Transactions:**
    - Fund transfers via [[Pay-to-PubKey-Hash (P2PKH)]], requiring a signature to spend.
2. **Data Carriage:**
    - Using OP_RETURN scripts for embedding metadata or tokens.
3. **Smart Contracts:**
    - Complex spending conditions enabled by [[Bitcoin Script]] or [[sCrypt]].
4. **Micropayments and IoT:**
    - VOUT allows atomic and programmable transfers for advanced use cases.

---

## Tags

#VOUT #UTXO #BitcoinScript #Transactions #Satoshis #LockingScript #TXID #Blockchain #DataStorage #DigitalSignatures

---

## See Also

- [[TXID]]
- [[Bitcoin Transactions]]
- [[UTXO]]
- [[lockScript]]
- [[Bitcoin Script]]
- [[Double-Spending]]
- [[OP_RETURN]]
- [[Satoshis]]