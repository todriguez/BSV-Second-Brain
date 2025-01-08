**`OP_PUSH_TX`** is a technique in [[Bitcoin Script]] that leverages [[ECDSA|ECDSA signature]] messages to enforce transactional states and conditions. This method enables sophisticated validation and control over transaction behavior by requiring the inclusion of the transaction pre-image in the script.

---

## How OP_PUSH_TX Works

`OP_PUSH_TX` requires the [[UTXO]] spender to provide the [[transaction pre-image]] (used to generate the signature) as part of the input [[ScriptSig|scriptSig]]. This pre-image can be included:

- As a single contiguous blob.  
- As multiple separate elements.  
- As a partial set, with the remaining elements defined by the output’s [[ScriptPubKey|scriptPubKey]].

### Validation Process

1. **Inclusion of the Pre-Image**:  
   The transaction pre-image is pushed onto the stack during execution.

2. **Signature Verification**:  
   The pre-image is hashed and signed, and the signature is validated using opcodes like [[OP_CHECKSIG]] or [[OP_CHECKSIGVERIFY]].  
   
3. **SIGHASH Flags**:  
   The [[SIGHASH Flags]] applied to the signature allow the validation of transaction properties, such as:
   - The number of inputs and outputs.  
   - Output script types and values.  
   - [[nSequence]] and [[nLockTime]] conditions.

---

## Use Cases

### **Finite State Machines**

In [[Smart Contract]] and [[Token Representations]], `OP_PUSH_TX` enables the creation of Turing-complete machines by treating the [[BSV Blockchain|blockchain]] ledger as an unbounded tape. Each output represents a state, while the input transactions dictate the next state.

### **Transaction State Enforcement**

`OP_PUSH_TX` allows enforcing conditions on:
- Input values and properties (e.g., nSequence, value).  
- Output scripts and values.  
- Transition scripts for the UTXO being spent, ensuring valid next states in multi-step operations.

### **Dynamic Smart Contracts**

By combining transaction pre-images with script evaluation, `OP_PUSH_TX` enables:
- **Conditional Execution**: Validating complex conditions before spending UTXOs.  
- **On-Chain Logic**: Enforcing state transitions directly on the [[BSV Blockchain|blockchain]] consensus layer.

---

## Technical Details
### [[Elliptic Curve]] Signature and Pre-Image

The pre-image includes various transaction elements such as inputs, outputs, values, and [[nLockTime]]. The signature is generated using the following [[ECDSA]] process:

1. **Keypair Generation**:  
   A private key $S$ is used to generate the public key $P$ using:  
   $$P = S \cdot G$$  
   where $G$ is the generator point on the elliptic curve.

2. **Signature Calculation**:  
   $$s = k^{-1} \cdot \left(H(m) + S \cdot r\right) \mod n$$  
   where:  
   - $H(m)$: Double SHA-256 hash of the transaction pre-image.  
   - $r$: The $x$-coordinate of $R = k \cdot G$.  
   - $k$: Ephemeral key.

3. **Validation**:  
   The signature is verified using `OP_CHECKSIGVERIFY`, ensuring the transaction matches the conditions encoded in the pre-image.



---

## Optimized Versions

### **Optimal OP_PUSH_TX**

- Uses predefined values for the private and ephemeral keys.  
- Simplifies computation, reducing script size to under 100 bytes.  
- Requires Low-S signatures to avoid failure, which may necessitate malleating transaction elements.

### **Classic OP_PUSH_TX**

- Changes signature endianness to ensure Low-S values.  
- Reduces failure rates to 1/256.  
- Provides greater robustness at the cost of slightly larger script size.

---

## Advantages

- **Turing Completeness**: Enables the creation of programmable contracts and [[Finite State Machines]].  
- **Precise Validation**: Enforces exact transaction properties at the consensus layer.  
- **Dynamic Capability**: Adapts to various use cases like [[Payment Channel]] and token operations.

---

## Tags

- [[OP_PUSH_TX]]  
- [[Bitcoin Script]]  
- [[ECDSA]]  
- [[SIGHASH Flags]]  
- [[Smart Contract]]  
- [[Finite State Machines]]  
- [[Token Representations]]  
- [[UTXO]]  
- [[nLockTime]]  
- [[nSequence]]  
- [[Transaction Validation]]  
