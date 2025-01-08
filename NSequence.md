# [[nLockTime]] and [[nSequence]]

[[nLockTime]] and [[nSequence]] are interlocks that can be applied to [[Bitcoin Transactions|Bitcoin Transactions]] to control the conditions under which transactions are accepted into a [[Block|block]].

---

## [[nSequence]]

**nSequence** is a parameter applied to each [[Bitcoin Transactions|input]] of a transaction. If a transaction’s [[nLockTime]] interlock is active (i.e., [[nLockTime]] is set to a point in the future), and one or more inputs have an `nSequence` value less than `UINT_MAX` (`0xFFFFFFFF`), the transaction cannot be accepted into a [[Block|block]].  

- **Non-Final Transactions**: Transactions with an active [[nLockTime]] and non-maximum `nSequence` values are marked as **non-final**. These remain unconfirmed until the conditions defined by [[nLockTime]] and `nSequence` are satisfied.

---

## [[nLockTime]]

**nLockTime** is a parameter applied to each transaction, specifying a future condition based on **Unix time** or **block height**. Before this specified point, the transaction is not eligible for inclusion in a block.  

### Conditions for [[nLockTime]]:

1. **All Inputs Finalized**:  
   If all inputs in a transaction have `nSequence = UINT_MAX` (`0xFFFFFFFF`), then `nLockTime` is ignored.

2. **Block Height vs. Unix Timestamp**:  
   - If `nLockTime < 500,000,000`: The integer is interpreted as a **block height**.  
   - If `nLockTime >= 500,000,000`: The integer is interpreted as a **Unix timestamp**.

The [[Unix Timestamp]] is the number of seconds elapsed since 00:00:00 UTC on 1 January 1970, excluding leap seconds. It simplifies time calculations by treating every day as 86,400 seconds.

---

## Use in [[Payment Channel]]

[[nLockTime]] and [[nSequence]] enable advanced functionalities like building [[Payment Channel|payment channels]].  

### Non-Final Transactions in Payment Channels:

- **Conditions for Non-Finality**:  
  Transactions with [[nLockTime]] set to a future point and at least one input having an `nSequence < 0xFFFFFFFF` are **non-final**. These transactions are held in a [[Transaction_Pools|transaction pool]] until:  
  - The specified [[nLockTime]] expires.  
  - All inputs have their `nSequence` values finalized (set to `UINT_MAX`).  

- **Transaction Replacement**:  
  Non-final transactions can be replaced with new versions that use the same inputs but have higher `nSequence` values. This mechanism enables parties to exchange updated transaction states dynamically without broadcasting every intermediate state to the blockchain.

### Benefits in Peer-to-Peer Networks:

By leveraging [[nLockTime]] and [[nSequence]], [[Payment Channel|payment channels]] facilitate secure and efficient off-chain interactions. Participants can exchange transaction updates in a [[Peer-to-Peer|peer-to-peer]] manner and only broadcast the final state for on-chain settlement.

---

## Tags
- [[nLockTime]]
- [[nSequence]]
- [[Bitcoin Transactions]]
- [[Block]]
- [[Unix Timestamp]]
- [[Transaction Pools]]
- [[Payment Channel]]
- [[Peer to Peer]]
- [[Time Locks]]
- [[Scalability]]
