# Pushdata Opcodes

## Overview

**Pushdata Opcodes** are a set of opcodes in [[Bitcoin Script]] that allow arbitrary data to be pushed onto the stack. These opcodes are crucial for constructing and manipulating byte vectors in Bitcoin transactions. They enable flexibility in [[lockScript]] and [[unlockScript]] design, supporting both standard and complex use cases.

Pushdata opcodes are often not explicitly shown in assembly representations of Bitcoin scripts but are automatically inserted by the script interpreter when pushing raw data. They are integral to the script execution process and support various data sizes, from small byte vectors to large datasets.

---

## Types of Pushdata Opcodes

There are several pushdata opcodes, each optimized for different data lengths:

### 1. **OP_PUSHDATA1**
- Used for pushing byte vectors between **76 bytes** and **255 bytes** in length.
- Requires an additional byte to specify the data length.

### 2. **OP_PUSHDATA2**
- Used for pushing byte vectors up to **65,535 bytes** in length.
- Requires two additional bytes to specify the data length.

### 3. **OP_PUSHDATA4**
- Supports pushing byte vectors up to **4,294,967,295 bytes** (4 GiB) in length.
- Requires four additional bytes to specify the data length.
- Matches the size constraints of [[IPv6]] jumbograms, making it suitable for handling large datasets or payloads in certain networking applications.

---

## How Pushdata Opcodes Work

When a pushdata opcode is encountered, the script interpreter:
1. Reads the length specifier (1, 2, or 4 bytes) following the opcode.
2. Reads the specified number of bytes from the script.
3. Pushes the extracted byte vector onto the stack.

For example:
- A script containing `OP_PUSHDATA1 0x0a "hello world"` pushes the string `"hello world"` onto the stack.

---

## Pushdata and Assembly Representation

In script assembly (ASM), pushdata opcodes are often abstracted for simplicity. Instead of explicitly writing `OP_PUSHDATA1`, raw data is typically represented directly, and the appropriate opcode is inferred by the interpreter.

For instance:
- In ASM, a data push like `0x6a 0x0a "hello world"` is written simply as `6a "hello world"`.
- The interpreter automatically uses `OP_PUSHDATA1` because the data length exceeds the limit of direct pushes.

---

## Use Cases for Pushdata Opcodes

### 1. **Data Embedding**
- Pushdata opcodes allow arbitrary data to be included in transaction scripts, such as in [[OP_RETURN]] outputs.

### 2. **Custom Smart Contracts**
- Complex [[Bitcoin Script]] contracts leverage pushdata opcodes for passing parameters and constructing conditions.

### 3. **Large Payloads**
- [[OP_PUSHDATA4]] supports extremely large datasets, aligning with [[IPv6]] jumbogram specifications for large network packets.

---

## Efficiency Considerations

1. **Compact Data Pushes**:
   - When possible, smaller pushdata opcodes (e.g., direct pushes or `OP_PUSHDATA1`) are preferred for efficiency.
   - Larger opcodes like `OP_PUSHDATA4` should only be used when necessary due to their additional overhead.

2. **Alignment with Protocols**:
   - The flexibility of pushdata opcodes ensures compatibility with both small scripts and applications requiring extensive data handling.

---

## Tags

#PushdataOpcodes #BitcoinScript #OP_PUSHDATA #IPv6 #BSV #Blockchain #ScriptExecution #DataManipulation

---

## See Also

- [[Bitcoin Script]]
- [[lockScript]]
- [[unlockScript]]
- [[OP_RETURN]]
- [[IPv6]]
- [[UTXO Model]]
