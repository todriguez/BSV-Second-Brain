Bitcoin uses a scripting system to define and validate the conditions under which [[UTXO|spendable transaction outputs (STOs)]] can be transferred. This scripting language, called **Script**, is simple, stack-based, and processes instructions sequentially from left to right. Similar to the [[Forth Programming Language|Forth programming language]], Bitcoin Script uses a stack to perform operations via [[Opcodes|opcodes]], with data pushed onto the stack and manipulated according to specified rules.

## Script as a State Machine

Although Bitcoin Script lacks explicit looping functions, it supports powerful computational constructs. **Finite State Machines** (FSMs) can be implemented by storing state information in one or more [[UTXO|UTXOs]]. These FSMs can:

1. **Receive input** from external [[Oracles|oracles]] or data embedded in the blockchain.
2. **Generate pseudo-random values** deterministically.
3. **Reference previous transactions** on the ledger to determine state transitions.

A loop is effectively formed by repeatedly checking input conditions and updating the UTXO state. Techniques like `[[OP_PUSH_TX]]` leverage [[ECDSA|ECDSA signatures]] to enforce specific conditions for subsequent transactions. The Bitcoin ledger acts as an **unbounded ticker tape**, enabling a series of computations until a halting condition is met.

## How Bitcoin Script Works

A transaction output script defines a **predicate**—a set of instructions describing how the tokens it locks can be unlocked. For example, a standard [[P2PKH|Pay-to-Public-Key-Hash (P2PKH)]] script requires the spender to provide:

1. A public key that hashes to the embedded [[Address|address]].
2. A valid [[Digital Signature|signature]] matching the private key corresponding to the public key.

### Flexibility in Scripting

Bitcoin Script enables customized conditions for unlocking tokens:

- Multi-signature requirements (e.g., [[OP_CHECKMULTISIG]]).
- Time-locked conditions (e.g., [[OP_CHECKLOCKTIMEVERIFY]]).
- Scripts requiring data or external input instead of keys.

The tokens are unlocked if the final value on the stack after executing the script is non-zero.

## Node Processing and Script Validation

Bitcoin Script is executed by nodes using a **script evaluation engine** with two primary stacks:

1. The **main stack**: Holds primary data and intermediate results.
2. The **alt stack**: Stores auxiliary data for specific operations.

These stacks support byte vectors for numerical and logical operations:

- Byte vectors are interpreted as **[[little-endian]] integers**.
- **Zero** can be represented as a null-length vector, 0x80 (negative zero), or any length of hexadecimal zeros.
- Non-zero values represent **True**, while any representation of zero is **False**.

### Pre-Genesis and Post-Genesis Differences

Before the [[Genesis Upgrade]], Script imposed limits on:

- **Stack size**: Limited to 520 bytes.
- **Integer length**: Integer operations used values no more than 4 bytes.

After Genesis:

- Data limits are defined by miners' economic policies rather than protocol rules.
- Larger data items can be concatenated and processed using [[Pushdata Opcodes|pushdata opcodes]].

## Expanding Script Functionality

Bitcoin Script evolves as network nodes collectively agree on new [[Opcodes|opcodes]] and data limits. For example:

- [[OP_RETURN]] supports adding arbitrary data to the blockchain.
- Mathematical operations and flow control constructs allow for complex scripts.

## Examples and Resources

### Key Concepts

1. [[Opcodes Used in Bitcoin Script|Opcodes]].
2. [[Number Encoding in Bitcoin Script|Number Encoding]].
3. [[Scripts with Flow Control (Conditional Clauses)|Scripts with Flow Control]].
4. [[OP_CODESEPARATOR|OP_CODESEPARATOR]].

### Complex Examples

Explore [[Complex Script Examples|examples]] showcasing advanced scripting techniques.

---

### Attribution

This content is based on the [Bitcoin Wiki article on Script](https://en.bitcoin.it/wiki/Script) under a [Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/), with substantial revisions to reflect [[BSV Blockchain]] features.