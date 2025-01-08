# sCrypt-TS

**sCrypt-TS** is an **embedded Domain Specific Language (eDSL)** based on [[TypeScript]] designed for writing smart contracts on [[Bitcoin]]. It bridges the gap between Bitcoin Script's low-level functionality and modern development environments, enabling developers to create secure, scalable, and expressive smart contracts with ease.

---

## Overview

### Embedded Domain Specific Language (eDSL)
sCrypt-TS is a subset of [[TypeScript]], meaning:
- All sCrypt code is valid TypeScript, but not all TypeScript code is valid sCrypt.
- It leverages TypeScript’s familiarity and type safety, providing a seamless learning curve for JavaScript developers.

### Purpose
sCrypt-TS abstracts the complexities of [[Bitcoin Script]], enabling developers to:
- Write sophisticated smart contracts efficiently.
- Compile human-readable code into low-level scripts executed by the [[Bitcoin Virtual Machine (BVM)]].

### Integration with Bitcoin
Smart contracts created with sCrypt-TS operate within Bitcoin's [[UTXO Model]]:
- Outputs act as locks via **locking scripts**.
- Inputs provide the keys via **unlocking scripts**.
- sCrypt-TS compiles high-level logic into locking scripts, allowing for advanced [[Predicates]] that define spending conditions.

---

## Key Features

### 1. High-Level Language
sCrypt-TS simplifies the development process:
- Developers write expressive, readable code.
- Contracts are compiled into low-level Bitcoin Script, ensuring network compatibility.

### 2. Extensibility
- Includes support for advanced scripting via [[sCrypt-TS Libraries]].
- Supports [[Static Analysis]] and tooling for debugging and testing.

### 3. Rich Type System
- Enables type safety for contract variables.
- Supports fixed-size arrays, user-defined types, and domain-specific types (e.g., [[PubKey]], [[Sig]]).

### 4. Integration with TypeScript
- The [[sCrypt]] language can be used as a standalone tool or embedded directly into TypeScript projects.
- sCrypt-TS seamlessly integrates on-chain and off-chain logic in a single language.

---

## How sCrypt-TS Works

### Compilation to Bitcoin Script
sCrypt-TS code is compiled into [[Bitcoin Script]], a stack-based language used to validate transactions. The resulting scripts:
- Serve as locking conditions for UTXOs.
- Are executed by the [[Bitcoin Virtual Machine]] when unlocking inputs.

### Using the `bsv` Submodule
sCrypt-TS includes a `bsv` submodule for managing Bitcoin primitives:
- Keypair generation.
- Transaction construction.
- Signing and serialization.

For example:
```typescript
import { bsv } from 'scrypt-ts';

const privKey = bsv.PrivateKey.fromRandom();
const pubKey = privKey.toPublicKey();
console.log(pubKey.toAddress().toString());
```

## Smart Contracts with sCrypt-TS

### Defining Smart Contracts

A smart contract is defined as a TypeScript class extending `SmartContract`. Example:

```

import { SmartContract, method, prop, assert } from "scrypt-ts";

class MyContract extends SmartContract {
  @prop()
  readonly value: bigint;

  constructor(value: bigint) {
    super(...arguments);
    this.value = value;
  }

  @method()
  public unlock(input: bigint) {
    assert(input === this.value, "Invalid input");
  }
}

```

### Properties and Methods

- **Properties** (`@prop`): Store on-chain data.
- **Methods** (`@method`): Define contract behavior, enforce conditions using [[assert]].

### Public and Non-Public Methods

- Public methods can be invoked externally (e.g., `unlock`).
- Non-public methods are internal, reusable within the contract.
## Advantages of sCrypt-TS

### 1. **Ease of Use**

- Abstracts away the complexity of raw Bitcoin Script.
- Compatible with modern development practices.

### 2. **Security**

- Avoids pitfalls like infinite loops by leveraging Bitcoin's script design.
- Built-in static analysis prevents common errors.

### 3. **Flexibility**

- Supports advanced use cases, such as:
    - [[Multi-Signature Transactions]].
    - [[Time-Locked Contracts]].
    - Iterative computations using techniques like [[OP_PUSHTX]] for unrolling loops across transactions.

### 4. **Efficiency**

- Contracts are lightweight and directly executable on Bitcoin’s blockchain.
- Optimized for [[Scalability]] via the UTXO model.

---

## Why Use sCrypt-TS?

1. **Aligned with Bitcoin’s Principles**:
    - Focuses on the intended design of Bitcoin as defined in the [[Bitcoin Whitepaper]].
    - Promotes lawful and scalable applications.
2. **Powerful Tooling**:
    - The [[sCrypt CLI]] simplifies project creation, testing, and deployment.
    - Integrated with familiar tools like [[Mocha]] for testing and [[Prettier]] for code formatting.
3. **Proven Capability**:
    - [[Project Babbage]] demonstrated sCrypt-TS’s flexibility by building a CPU emulator entirely in Bitcoin Script.

---

## Tags

#sCrypt #sCryptTS #SmartContracts #BitcoinScript #BSV #UTXOModel #TypeScript #ProgrammableMoney #Scalability #bsv

---

## See Also

- [[Bitcoin Script]]
- [[UTXO Model]]
- [[OP_PUSHTX]]
- [[sCrypt-TS Libraries]]
- [[Smart Contract]]
- [[Bitcoin Virtual Machine]]