
[[nLockTime]] and [[nSequence]] are two parameters in the [[Bitcoin Transactions|Bitcoin transaction]] structure. They control when and how a transaction can be accepted into a [[Block|block]], enabling time-based constraints and more flexible transaction flows. Both fields also form the basis for many [[Time Lock|time-locked]] features and [[Smart Contract]] in [[BSV Blockchain]].

---

## nLockTime

### Overview

[[nLockTime]] is part of a transaction’s data structure. It specifies a point (either in terms of block height or Unix timestamp) before which the transaction is not valid for inclusion in a block. If **all inputs** in a transaction have [[nSequence]] = `0xFFFFFFFF` (UINT_MAX), then `nLockTime` is ignored entirely.

### Block-Height vs. Timestamp

- **Block Height**:  
  If `nLockTime < 500,000,000`, it represents the block height from which the transaction becomes valid.

- **Unix Timestamp**:  
  If `nLockTime >= 500,000,000`, it represents the Unix epoch timestamp. The transaction is valid once the median timestamp of the last 11 blocks exceeds this value.

### Usage in Time-Locked Transactions

By setting `nLockTime` to a future block or time, the transaction’s outputs remain locked until that moment is reached. This mechanism enables various forms of [[Time Lock|time-lock]]-based scripts and contracts.

---

## nSequence

### Overview

[[nSequence]] is attached to each [[Bitcoin Transactions|input]] in a transaction. Initially, it was designed for updating or replacing transactions before they were mined. With [[BIP68]], it gained the capacity to set **relative lock times**, specifying how long after a particular input’s confirmation a transaction can be spent.

### Non-Final Transactions

If any input has `nSequence < 0xFFFFFFFF` and the transaction’s [[nLockTime]] is set to a future point, the transaction is marked as **[[non-final]]**. Such transactions will not be accepted into a block until their conditions (time or block height) are satisfied.

### Relative Lock Time

Depending on the 22nd bit in `nSequence`:
- **Bit = 0**: Interpreted as **block-based** relative lock time.  
- **Bit = 1**: Interpreted as **time-based** (seconds).

This approach allows more granular control than the absolute constraints of [[nLockTime]].

---

## Use in Payment Channels

When a transaction has `nLockTime` set to the future, and at least one input has `nSequence < 0xFFFFFFFF`, the transaction is considered **non-final** and may remain in a [[Transaction_Pools|transaction pool]]. Participants can replace it with a version containing a higher `nSequence`. This functionality is integral to many [[Payment Channel|payment channel]] protocols, letting parties exchange updated transaction states privately before broadcasting the final state on-chain.

---

## Tags
- #nlocktime
- #nsequence
- #bitcoin
- #transactions
- #time-lock
- #smart-contracts
- #payment-channels
- #block
- #transaction-pools
