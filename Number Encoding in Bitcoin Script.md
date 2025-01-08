# Number Encoding in Bitcoin Script

Bitcoin Script, the stack-based programming language used in [[BSV Blockchain]], employs unique conventions for encoding and manipulating numeric values. These conventions are essential for ensuring consistent behavior across the network and avoiding ambiguities during transaction validation.

---

## Overview of Number Encoding

1. **Little-Endian Representation**:
   - Numbers in Bitcoin Script are encoded in **[[little-endian]]** [[byte]] order.
   - This means the least significant byte (LSB) appears first in memory.

2. **Variable-Length Encoding**:
   - Numbers are stored in their minimal byte-length representation.
   - Leading zero bytes are stripped, except when required for representing the sign.

3. **Two's Complement**:
   - Negative numbers are encoded using **two's complement** notation.
   - The most significant bit (MSB) of the final byte is used as the **sign bit**:
     - `0`: Positive or zero.
     - `1`: Negative.

4. **[[Minimal Encoding Rule]]**:
   - Numbers must be encoded in the smallest number of bytes possible while retaining their value.
   - Leading zero bytes are prohibited, and the sign bit is set only when necessary.

---

## Encoding Rules

### Positive Numbers
- Positive numbers are represented as their hexadecimal equivalent in little-endian format.
- Example:
  - Decimal `5` → Hexadecimal `05` → Encoded as `0x05`.

### Negative Numbers
- Negative numbers are encoded using the sign bit in the MSB of the last byte.
- Example:
  - Decimal `-5` → Hexadecimal `05` → Encoded as `0x85` (last byte's MSB is set).

### Zero
- The number zero is represented as an empty byte string (`0x`).
- This ensures minimal encoding and reduces unnecessary data.

### Special Cases
- If the MSB of the most significant byte is `1` for a positive number, an extra `00` byte is prepended to distinguish it from a negative number.
- Example:
  - Decimal `128` → Hexadecimal `0x80` → Encoded as `0x8000` (to prevent confusion with `-128`).

---

## Operations on Encoded Numbers

1. **Pushing Numbers**:
   - Use [[PUSHDATA]] opcodes to place encoded numbers onto the stack.
   - Minimal encoding ensures efficient usage of stack space.

2. **Arithmetic Operations**:
   - Script operators like [[OP_ADD]], [[OP_SUB]], [[OP_MUL]], and [[OP_DIV]] use encoded numbers as inputs.
   - Operands are decoded, the operation is performed, and the result is re-encoded.

3. **Comparison Operations**:
   - Operators like [[OP_EQUAL]], [[OP_GREATERTHAN]], and [[OP_LESSTHAN]] rely on the same encoding rules for consistent behavior.

4. **Verification of Minimal Encoding**:
   - The [[OP_CHECKSIG]] and related operations enforce the minimal encoding rule to prevent non-standard transactions.

---

## Examples

### Encoding Positive Numbers
| Decimal | Hexadecimal (LE) | Encoded |
|---------|------------------|---------|
| `0`     | `0x`             | `0x`    |
| `1`     | `0x01`           | `0x01`  |
| `256`   | `0x0100`         | `0x0100`|

### Encoding Negative Numbers
| Decimal | Hexadecimal (LE) | Encoded |
|---------|------------------|---------|
| `-1`    | `0x01`           | `0x81`  |
| `-128`  | `0x80`           | `0x80`  |
| `-129`  | `0x8100`         | `0x8100`|

### Handling Edge Cases
| Decimal | Hexadecimal (LE) | Encoded |
|---------|------------------|---------|
| `127`   | `0x7F`           | `0x7F`  |
| `128`   | `0x80`           | `0x8000`|

---

## Importance of Number Encoding

1. **[[Consensus Rules]]**:
   - Consistent number encoding ensures nodes interpret and validate transactions identically.

2. **Efficiency**:
   - Minimal encoding reduces the size of scripts, improving processing efficiency and minimizing transaction fees.

3. **Security**:
   - Strict encoding prevents malleability attacks, where alternative encodings of the same number could alter transaction behavior.

4. **Compatibility**:
   - Following these conventions ensures scripts execute predictably across all BSV implementations.

---

## Tags

#BitcoinScript #NumberEncoding #BSV #ConsensusRules #StackOperations #ScriptValidation

---

## See Also

- [[Bitcoin Script]]
- [[PUSHDATA]]
- [[OP_ADD]]
- [[OP_CHECKSIG]]
- [[Script Malleability]]
- [[Little-Endian Encoding]]
