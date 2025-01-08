# Integer

## General Definition

An **integer** is a whole number that can be positive, negative, or zero. Integers belong to the set of numbers denoted as $( \mathbb{Z} )$, which includes:
- Positive integers $(1, 2, 3, \ldots)$
- Negative integers $(-1, -2, -3, \ldots)$
- Zero $(0)$

### Properties of Integers

1. **Arithmetic Operations**:
   - Integers are closed under addition, subtraction, and multiplication.
   - Division may not yield an integer (e.g., $(7 \div 2 = 3.5)$.

2. **Ordering**:
   - Integers are ordered, meaning they can be compared using $<$, $>$, $\leq$ , and $\geq$.

3. **Applications**:
   - Used in counting, indexing, and mathematical modeling.

---

## Integers in BSV

In the context of the [[BSV Blockchain]] blockchain, integers are used extensively to represent values like:
- [[Satoshis]] (the smallest unit of Bitcoin).
- Lock times and sequence numbers in [[Bitcoin Transactions]].
- Arguments and results in [[Bitcoin Script]] operations.

### Representation in Bitcoin Script

1. **Little-Endian Encoding**:
   - Integers in [[Bitcoin Script]] are encoded in **[[little-endian]]** format, meaning the least significant byte (LSB) comes first.
   - Example: $5$ is represented as `0x05`.

2. **Variable-Length Encoding**:
   - Integers are stored in their minimal byte-length representation, omitting leading zero bytes unless required for the sign bit.

3. **Sign Bit for Negative Integers**:
   - [[Negative integers]] are represented using the **two's complement** convention, where the most significant bit (MSB) of the last byte indicates the sign:
     - \(0\): Positive or zero.
     - \(1\): Negative.

### Negative Integer Representation

- To represent a negative integer:
  1. Take the absolute value of the number.
  2. Convert it to its hexadecimal little-endian form.
  3. Set the MSB of the last byte to \(1\) to indicate negativity.

#### Example:
- Decimal \(-5\):
  - Absolute value: \(5\).
  - Hexadecimal (little-endian): `0x05`.
  - Add sign bit: `0x85`.

---

## Examples of Integer Representation in BSV

| Decimal | Little-Endian Hex | Representation Type |
|---------|-------------------|---------------------|
| \(0\)   | `0x`              | Zero               |
| \(1\)   | `0x01`            | Positive           |
| \(-1\)  | `0x81`            | Negative           |
| \(128\) | `0x8000`          | Positive (extra byte for MSB) |
| \(-128\)| `0x80`            | Negative           |

---

## Operations with Integers in Bitcoin Script

1. **Arithmetic**:
   - Operations like addition (\[[OP_ADD]]\), subtraction (\[[OP_SUB]]\), and multiplication (\[[OP_MUL]]\) are performed on integers.

2. **Comparison**:
   - Bitcoin Script supports integer comparison using operators like \[[OP_EQUAL]], \[[OP_GREATERTHAN]], and \[[OP_LESSTHAN]].

3. **Bounds**:
   - Integer sizes are limited by script execution constraints to ensure computational safety.

---

## Applications of Integers in BSV

1. **Transaction Values**:
   - Every transaction output specifies a value in satoshis, represented as an integer.

2. **Locking and Unlocking Conditions**:
   - Used in [[Bitcoin Script]] for time locks, multi-signature thresholds, and other predicates.

3. **Complex Logic**:
   - Implementing logic for [[Smart Contract]] often requires integer-based computations.

---

## Tags

#Integer #BitcoinScript #BSV #TwoComplement #Encoding #TransactionValues #SmartContracts #Arithmetic

---

## See Also

- [[Bitcoin Script]]
- [[Two's Complement]]
- [[Little-Endian Encoding]]
- [[Bitcoin Transactions]]
- [[Satoshis]]
- [[Smart Contract]]
