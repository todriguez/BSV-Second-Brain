## General Principles

1. **Truth Values:**
    
    - `False`: Defined as zero, negative zero, or an empty array.
    - `True`: Defined as anything else.
2. **OP_NOP (No Operation):**
    
    - Opcodes such as [[OP_NOP1]] to [[OP_NOP10]] were originally reserved for future use in cryptographic functions as technology evolves.


# Constants

When talking about scripts, these value-pushing words are usually
omitted.

| **Word**             | **Opcode**     | **Hex**   | **Input** | **Output**    | **Description**                                                                           |
| -------------------- | -------------- | --------- | --------- | ------------- | ----------------------------------------------------------------------------------------- |
| OP_0, OP_FALSE       | 0              | 0x00      | Nothing   | (empty value) | Pushes an empty array of bytes onto the stack. Not a no-op: it adds an item to the stack. |
| [[Pushdata_Opcodes]] | Push]]1-75     | 1-75      | 0x01-0x4b | (special)     | Data                                                                                      |
| [[Pushdata_Opcodes]] | OP_PUSHDATA1]] | 76        | 0x4c      | (special)     | Data                                                                                      |
| [[Pushdata_Opcodes]] | OP_PUSHDATA2]] | 77        | 0x4d      | (special)     | Data                                                                                      |
| [[Pushdata_Opcodes]] | OP_PUSHDATA4]] | 78        | 0x4e      | (special)     | Data                                                                                      |
| OP_1NEGATE           | 79             | 0x4f      | Nothing   | -1            | Pushes the number `-1` onto the stack.                                                    |
| OP_1, OP_TRUE        | 81             | 0x51      | Nothing   | 1             | Pushes the number `1` onto the stack.                                                     |
| OP_2-OP_16           | 82-96          | 0x52-0x60 | Nothing   | 2-16          | Pushes the corresponding number (2-16) onto the stack.                                    |

  ----------------------------------------------------------------- -------- ----------- ----------- --------------- ---------------------------------------------------------------------------------------------------------

# Flow Control 

| **Word**                   | **Opcode** | **Hex** | **Input**    | **Output**       | **Description**                                                                                    |
| -------------------------- | ---------- | ------- | ------------ | ---------------- | -------------------------------------------------------------------------------------------------- |
| **OP_NOP**                 | 97         | 0x61    | Nothing      | Nothing          | Does nothing.                                                                                      |
| **OP_VER (DISABLED)**      | 98         | 0x62    | Nothing      | Protocol version | Protocol version-related operation (disabled in BSV).                                              |
| **OP_IF**                  | 99         | 0x63    | [expression] | -                | Executes enclosed statements if the top stack value is `True`.                                     |
| **OP_NOTIF**               | 100        | 0x64    | [expression] | -                | Executes enclosed statements if the top stack value is `False`.                                    |
| **OP_VERIF (DISABLED)**    | 101        | 0x65    | (DISABLED)   | -                | Disabled opcode.                                                                                   |
| **OP_VERNOTIF (DISABLED)** | 102        | 0x66    | (DISABLED)   | -                | Disabled opcode.                                                                                   |
| **OP_ELSE**                | 103        | 0x67    | -            | -                | Executes the alternative block if the preceding `OP_IF` or `OP_NOTIF` condition was `False`.       |
| **OP_ENDIF**               | 104        | 0x68    | -            | -                | Marks the end of a conditional block. All blocks must end, or the transaction is invalid.          |
| **OP_VERIFY**              | 105        | 0x69    | True / False | Nothing / *fail* | Marks the transaction as invalid if the top stack value is not `True`.                             |
| **OP_RETURN**              | 106        | 0x6a    | Nothing      | *Ends execution* | Marks the transaction as invalid if executed. Can carry metadata in a provably unspendable output. |

---

# Stack Operations 

| **Word**            | **Opcode** | **Hex** | **Input**           | **Output**         | **Description**                                                     |
| ------------------- | ---------- | ------- | ------------------- | ------------------ | ------------------------------------------------------------------- |
| **OP_TOALTSTACK**   | 107        | 0x6b    | x1                  | (alt)x1            | Moves the top stack item to the alternate stack.                    |
| **OP_FROMALTSTACK** | 108        | 0x6c    | (alt)x1             | x1                 | Moves the top item from the alternate stack to the main stack.      |
| **OP_2DROP**        | 109        | 0x6d    | x1 x2               | Nothing            | Removes the top two stack items.                                    |
| **OP_2DUP**         | 110        | 0x6e    | x1 x2               | x1 x2 x1 x2        | Duplicates the top two stack items.                                 |
| **OP_3DUP**         | 111        | 0x6f    | x1 x2 x3            | x1 x2 x3 x1 x2 x3  | Duplicates the top three stack items.                               |
| **OP_2OVER**        | 112        | 0x70    | x1 x2 x3 x4         | x1 x2 x3 x4 x1 x2  | Copies the pair of items two spaces back in the stack to the front. |
| **OP_2ROT**         | 113        | 0x71    | x1 x2 x3 x4 x5 x6   | x3 x4 x5 x6 x1 x2  | Rotates the fifth and sixth items to the top of the stack.          |
| **OP_2SWAP**        | 114        | 0x72    | x1 x2 x3 x4         | x3 x4 x1 x2        | Swaps the top two pairs of items.                                   |
| **OP_IFDUP**        | 115        | 0x73    | x                   | x / x x            | Duplicates the top item if it is not zero.                          |
| **OP_DEPTH**        | 116        | 0x74    | Nothing             | <stack size>       | Pushes the number of stack items onto the stack.                    |
| **OP_DROP**         | 117        | 0x75    | x                   | Nothing            | Removes the top stack item.                                         |
| **OP_DUP**          | 118        | 0x76    | x                   | x x                | Duplicates the top stack item.                                      |
| **OP_NIP**          | 119        | 0x77    | x1 x2               | x2                 | Removes the second-to-top stack item.                               |
| **OP_OVER**         | 120        | 0x78    | x1 x2               | x1 x2 x1           | Copies the second-to-top stack item to the top.                     |
| **OP_PICK**         | 121        | 0x79    | xn ... x2 x1 x0 <n> | xn ... x2 x1 x0 xn | Copies the nth item from the stack to the top.                      |
| **OP_ROLL**         | 122        | 0x7a    | xn ... x2 x1 x0 <n> | ... x2 x1 x0 xn    | Moves the nth item from the stack to the top.                       |
| **OP_ROT**          | 123        | 0x7b    | x1 x2 x3            | x2 x3 x1           | Rotates the top three items to the left.                            |
| **OP_SWAP**         | 124        | 0x7c    | x1 x2               | x2 x1              | Swaps the top two items.                                            |
| **OP_TUCK**         | 125        | 0x7d    | x1 x2               | x2 x1 x2           | Copies the top item and inserts it before the second-to-top item.   |

---

# Data Manipulation 

| **Word**       | **Opcode** | **Hex**  | **Input**   | **Output**     | **Description**                                                           |
|-----------------|------------|----------|-------------|----------------|---------------------------------------------------------------------------|
| **OP_CAT**      | 126        | 0x7e     | x1 x2       | out            | Concatenates two strings.                                                |
| **OP_SPLIT**    | 127        | 0x7f     | x n         | x1 x2          | Splits byte sequence `x` at position `n`.                                |
| **OP_NUM2BIN**  | 128        | 0x80     | a b         | out            | Converts numeric value `a` into a byte sequence of length `b`.           |
| **OP_BIN2NUM**  | 129        | 0x81     | x           | out            | Converts byte sequence `x` into a numeric value.                         |
| **OP_SIZE**     | 130        | 0x82     | in          | in size        | Pushes the string length of the top element of the stack (without popping it). |

---

# Bitwise Logic 

| **Word**           | **Opcode** | **Hex**  | **Input**   | **Output**       | **Description**                                                         |
|---------------------|------------|----------|-------------|------------------|-------------------------------------------------------------------------|
| **OP_INVERT**       | 131        | 0x83     | in          | out              | Flips all the bits in the input.                                        |
| **OP_AND**          | 132        | 0x84     | x1 x2       | out              | Performs a boolean *AND* operation between each bit of the inputs.      |
| **OP_OR**           | 133        | 0x85     | x1 x2       | out              | Performs a boolean *OR* operation between each bit of the inputs.       |
| **OP_XOR**          | 134        | 0x86     | x1 x2       | out              | Performs a boolean *exclusive OR* operation between each bit of the inputs. |
| **OP_EQUAL**        | 135        | 0x87     | x1 x2       | True / false     | Returns `1` if the inputs are exactly equal, otherwise returns `0`.     |
| **OP_EQUALVERIFY**  | 136        | 0x88     | x1 x2       | Nothing / *fail* | Same as `OP_EQUAL`, but runs `OP_VERIFY` afterward.                     |


# Arithmetic

BitcoinScript supports arithmetic on bignum values A [[bignum]] is a byte sequence that represents a numeric value. The length of the byte sequence must be less than or equal to 750,000 bytes. Byte sequences larger than 750,000 bytes are valid in Bitcoin however current rules dictate that they are not recognised as a valid numeric value.

Note that while some operations require parameters to be valid numeric values, they may produce byte sequences which are not valid numeric values (for example, OP_MUL may produce a byte sequence which is too large to validly represent a numeric value).

| **Word**                | **Opcode** | **Hex**  | **Input**     | **Output**           | **Description**                                                                                      |
|--------------------------|------------|----------|---------------|----------------------|------------------------------------------------------------------------------------------------------|
| **OP_1ADD**             | 139        | 0x8b     | in            | out                  | Adds 1 to the input.                                                                                |
| **OP_1SUB**             | 140        | 0x8c     | in            | out                  | Subtracts 1 from the input.                                                                         |
| **OP_2MUL** **DISABLED**| 141        | 0x8d     | in            | out                  | Multiplies the input by 2. (Scheduled to be re-enabled in the Chronicle update.)                    |
| **OP_2DIV** **DISABLED**| 142        | 0x8e     | in            | out                  | Divides the input by 2. (Scheduled to be re-enabled in the Chronicle update.)                       |
| **OP_NEGATE**           | 143        | 0x8f     | in            | out                  | Flips the sign of the input.                                                                        |
| **OP_ABS**              | 144        | 0x90     | in            | out                  | Converts the input to a positive value.                                                             |
| **OP_NOT**              | 145        | 0x91     | in            | out                  | If the input is 0 or 1, it is flipped. Otherwise, the output will be 0.                             |
| **OP_0NOTEQUAL**        | 146        | 0x92     | in            | out                  | Returns 0 if the input is 0, otherwise returns 1.                                                   |
| **OP_ADD**              | 147        | 0x93     | a b           | out                  | Adds `a` to `b`.                                                                                   |
| **OP_SUB**              | 148        | 0x94     | a b           | out                  | Subtracts `b` from `a`.                                                                             |
| **OP_MUL**              | 149        | 0x95     | a b           | out                  | Multiplies `a` by `b`.                                                                              |
| **OP_DIV**              | 150        | 0x96     | a b           | out                  | Divides `a` by `b`.                                                                                 |
| **OP_MOD**              | 151        | 0x97     | a b           | out                  | Returns the remainder after dividing `a` by `b`.                                                    |
| **OP_LSHIFT**           | 152        | 0x98     | a b           | out                  | Performs a logical left shift of `b` bits on `a`.                                                   |
| **OP_RSHIFT**           | 153        | 0x99     | a b           | out                  | Performs a logical right shift of `b` bits on `a`.                                                  |
| **OP_BOOLAND**          | 154        | 0x9a     | a b           | out                  | Returns 1 if both `a` and `b` are not 0, otherwise returns 0.                                       |
| **OP_BOOLOR**           | 155        | 0x9b     | a b           | out                  | Returns 1 if either `a` or `b` is not 0, otherwise returns 0.                                       |
| **OP_NUMEQUAL**         | 156        | 0x9c     | a b           | out                  | Returns 1 if the numbers are equal, otherwise returns 0.                                             |
| **OP_NUMEQUALVERIFY**   | 157        | 0x9d     | a b           | Nothing / *fail*     | Same as `OP_NUMEQUAL`, but runs `OP_VERIFY` afterward.                                              |
| **OP_NUMNOTEQUAL**      | 158        | 0x9e     | a b           | out                  | Returns 1 if the numbers are not equal, otherwise returns 0.                                         |
| **OP_LESSTHAN**         | 159        | 0x9f     | a b           | out                  | Returns 1 if `a` is less than `b`, otherwise returns 0.                                              |
| **OP_GREATERTHAN**      | 160        | 0xa0     | a b           | out                  | Returns 1 if `a` is greater than `b`, otherwise returns 0.                                           |
| **OP_LESSTHANOREQUAL**  | 161        | 0xa1     | a b           | out                  | Returns 1 if `a` is less than or equal to `b`, otherwise returns 0.                                  |
| **OP_GREATERTHANOREQUAL**| 162       | 0xa2     | a b           | out                  | Returns 1 if `a` is greater than or equal to `b`, otherwise returns 0.                               |
| **OP_MIN**              | 163        | 0xa3     | a b           | out                  | Returns the smaller of `a` and `b`.                                                                 |
| **OP_MAX**              | 164        | 0xa4     | a b           | out                  | Returns the larger of `a` and `b`.                                                                  |
| **OP_WITHIN**           | 165        | 0xa5     | x min max     | out                  | Returns 1 if `x` is within the specified range (left-inclusive), otherwise returns 0.               |

  ----------------------- -------- ------ ----------- ------------------ ---------------------------------------------------------------------------------------------------

# Cryptography

| **Word**                | **Opcode** | **Hex**  | **Input**                                  | **Output**             | **Description**                                                                                                                                                                                                                                            |
|--------------------------|------------|----------|--------------------------------------------|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **OP_RIPEMD160**         | 166        | 0xa6     | in                                         | hash                  | Hashes the input using RIPEMD-160.                                                                                                                                                                                                                        |
| **OP_SHA1**              | 167        | 0xa7     | in                                         | hash                  | Hashes the input using SHA-1.                                                                                                                                                                                                                             |
| **OP_SHA256**            | 168        | 0xa8     | in                                         | hash                  | Hashes the input using SHA-256.                                                                                                                                                                                                                           |
| **OP_HASH160**           | 169        | 0xa9     | in                                         | hash                  | Hashes the input twice: first with SHA-256 and then with RIPEMD-160.                                                                                                                                                                                      |
| **OP_HASH256**           | 170        | 0xaa     | in                                         | hash                  | Hashes the input twice with SHA-256.                                                                                                                                                                                                                      |
| **OP_CODESEPARATOR**     | 171        | 0xab     | Nothing                                    | Nothing               | Marks a position in the script. All subsequent signature-checking operations will only validate against the data after the most recently executed `OP_CODESEPARATOR`.                                                                                     |
| **OP_CHECKSIG**          | 172        | 0xac     | sig pubkey                                | True / false          | Verifies that the signature is valid for the transaction hash and the given public key. Returns 1 if valid, 0 otherwise.                                                                                                                                  |
| **OP_CHECKSIGVERIFY**    | 173        | 0xad     | sig pubkey                                | Nothing / *fail*      | Same as `OP_CHECKSIG`, but runs `OP_VERIFY` afterward.                                                                                                                                                                                                    |
| **OP_CHECKMULTISIG**     | 174        | 0xae     | x sig1 sig2 ... \<n_sigs\> pub1 pub2 ...  | True / false          | Verifies multiple signatures against corresponding public keys. Returns 1 if all signatures are valid. Due to a bug, an extra unused value (x) is removed from the stack. Script spenders must account for this by adding a dummy value to the stack.     |
| **OP_CHECKMULTISIGVERIFY**| 175       | 0xaf     | x sig1 sig2 ... \<n_sigs\> pub1 pub2 ...  | Nothing / *fail*      | Same as `OP_CHECKMULTISIG`, but runs `OP_VERIFY` afterward.                                                                                                                                                                                               |

  -------------------------------------------------------------- -------- ------ ------------------------------------------------------------------------------------ ------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Used NOP opcode identifiers

In Bitcoin\'s history, new opcodes were added that used reserved NO_OP opcode identifiers. These opcodes have been reverted to the original OP_NOP functionality.

| **Word**     | **Opcode** | **Hex**  | **Input** | **Output** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------|------------|----------|-----------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **OP_NOP2**  | 177        | 0xb1     | Nothing   | Nothing    | NO OPERATION. Previously `OP_CHECKLOCKTIMEVERIFY`: Marks a transaction as invalid if the top stack item is greater than the transaction's `nLockTime` field. The script evaluation continues as though an `OP_NOP` was executed if the locktime conditions are met. Transaction is also invalid if: 1. The stack is empty; 2. The top stack item is negative; 3. The top stack item is greater than or equal to 500000000 while `nLockTime` is less than 500000000, or vice versa; 4. The input's `nSequence` field is `0xffffffff`. |
| **OP_NOP3**  | 178        | 0xb2     | Nothing   | Nothing    | NO OPERATION. Previously `OP_CHECKSEQUENCEVERIFY`: Marks a transaction as invalid if the relative lock time of the input (enforced by `nSequence`) is not equal to or longer than the value of the top stack item. The exact semantics are described in [BIP-0068](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki) and [BIP-0112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki).                                                                                               |


# Pseudo-Words

These words are used internally for assisting with transaction matching. They are invalid if used in actual scripts.

| Word                 | **Opcode** | **Hex** | **Description**                                        |
| -------------------- | ---------- | ------- | ------------------------------------------------------ |
| **OP_PUBKEYHASH**    | 253        | 0xfd    | Represents a public key hashed with `OP_HASH160`.      |
| **OP_PUBKEY**        | 254        | 0xfe    | Represents a public key compatible with `OP_CHECKSIG`. |
| **OP_INVALIDOPCODE** | 255        | 0xff    | Matches any opcode that is not yet assigned.           |


# Reserved Words

Any opcode not assigned is also reserved. Using an unassigned opcode makes the transaction **invalid**.

| **Word**                   | **Opcode**        | **Hex**         | **When Used**                                                                                      |
|----------------------------|-------------------|-----------------|----------------------------------------------------------------------------------------------------|
| **OP_RESERVED**            | 80                | 0x50            | **Transaction is invalid** unless occurring in an unexecuted `OP_IF` branch.                      |
| **OP_RESERVED1**           | 137               | 0x89            | **Transaction is invalid** unless occurring in an unexecuted `OP_IF` branch.                      |
| **OP_RESERVED2**           | 138               | 0x8a            | **Transaction is invalid** unless occurring in an unexecuted `OP_IF` branch.                      |
| **OP_NOP1**, **OP_NOP4-10**| 176, 179-185      | 0xb0, 0xb3-0xb9 | The word is ignored. Does not mark the transaction as invalid.                                     |



# Examples

For examples of common Bitcoin transaction scripts please see [[Bitcoin Transactions|Bitcoin Transactions]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Script](https://en.bitcoin.it/wiki/Script)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated we acknowledge the original authors.

Bitcoin Script is a stack-based programming language used to define the unlocking and locking conditions of [[Spendable Transaction Outputs (STOs)|STOs]]. Each operation within the script is represented by an [[opcode]] (operation code). Opcodes perform various tasks such as stack manipulation, arithmetic, cryptography, and flow control.

This document provides a comprehensive overview of opcodes categorized by their functionality. Each table lists the opcode’s word, hexadecimal representation, input, output, and a description of its function.