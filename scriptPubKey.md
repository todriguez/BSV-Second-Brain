# scriptPubKey

## Overview

In the context of [[BSV Blockchain]], a **scriptPubKey** is a type of [[lockScript]] that defines the conditions under which a specific [[UTXO]] (Unspent Transaction Output) can be spent. As its name implies, a scriptPubKey often involves a **public key** or its hashed representation to enforce spending conditions. It forms part of the output of a [[Bitcoin Transaction]] and is integral to [[Bitcoin Script]]'s predicate-based system.

---

## Relationship to Lock Scripts

A **lockScript** is a general term for a script that sets the conditions for unlocking a UTXO. A scriptPubKey is a specific implementation of a lockScript that usually includes a public key or its hash. For example:

1. The **Pay-to-PubKey-Hash (P2PKH)** scriptPubKey requires the spender to provide:
   - A matching [[public key]].
   - A valid [[digital signature]] derived from the corresponding [[private key]].

2. The **Pay-to-PubKey (P2PK)** scriptPubKey requires:
   - Only the provision of a matching public key and a valid signature.

---

## How scriptPubKey Works

1. **Creation**:
   - When a transaction creates a UTXO, it attaches a scriptPubKey to the output.
   - The scriptPubKey acts as a "lock" that defines the rules for spending that UTXO.

2. **Spending**:
   - To spend the UTXO, the corresponding [[unlockScript]] (or scriptSig) must provide data satisfying the scriptPubKey's conditions.
   - For instance, in P2PKH:
     - The unlockScript must contain a valid signature and the public key that hashes to the specified value in the scriptPubKey.

3. **Execution**:
   - The [[Bitcoin Virtual Machine (BVM)]] evaluates the combination of the unlockScript and scriptPubKey.
   - If the evaluation results in `true`, the UTXO is considered unlocked.

---

## Example: Pay-to-PubKey-Hash (P2PKH)

The **scriptPubKey** for a P2PKH UTXO typically looks like this:

```
OP_DUP OP_HASH160 <PubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

- **Explanation**:
    
    1. `OP_DUP`: Duplicates the public key on the stack.
    2. `OP_HASH160`: Hashes the duplicated key using [[RIPEMD-160]] after [[SHA-256]].
    3. `<PubKeyHash>`: Pushes the hashed public key to the stack (defined during UTXO creation).
    4. `OP_EQUALVERIFY`: Verifies that the hashed public key matches `<PubKeyHash>`.
    5. `OP_CHECKSIG`: Verifies the validity of the provided signature against the original public key.
- **UnlockScript**:
    
    - When spending the UTXO, the unlockScript (scriptSig) must provide:
 ```
<Signature> <PublicKey>
```

## Variants of scriptPubKey

1. **Pay-to-PubKey (P2PK)**:
    
    - A simpler variant where the scriptPubKey directly references the public key:
        `<PubKey> OP_CHECKSIG`

---

## Security Considerations

1. **Public Key Disclosure**:
    - In P2PKH, the public key is only revealed when the UTXO is spent, protecting it from attacks until then.
    - In P2PK, the public key is part of the scriptPubKey, exposing it earlier.
2. **Replay and Replacement Attacks**:
    - A properly crafted scriptPubKey ensures transactions are secure from tampering unless explicitly permitted (e.g., via [[Digital Asset Recovery (DAR)]]).

---

## Significance of scriptPubKey in BSV

- In [[BSV Blockchain]], scriptPubKey retains its original design and capabilities as envisioned in the [[Bitcoin Whitepaper]].
- With the restoration of [[Bitcoin Script]] opcodes, scriptPubKey can define a wide range of locking conditions, enabling advanced smart contracts and programmable money scenarios.

---

## Tags

#scriptPubKey #lockScript #BitcoinScript #BSV #UTXO #P2PKH #P2PK #Transactions

---

## See Also

- [[Bitcoin Script]]
- [[UTXO]]
- [[Bitcoin Transactions]]
- [[Pay-to-PubKey-Hash (P2PKH)]]
- [[Pay-to-Script-Hash (P2SH)]]
- [[Digital Asset Recovery (DAR)]]
- [[Bitcoin Virtual Machine (BVM)]]
- [[Public Key]]