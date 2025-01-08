
^bsv-difficulty-target
#BSV #Difficulty #Target #Mining #HashRate #Reference

This document provides a comprehensive overview of **how the difficulty target is calculated** in Bitcoin SV, incorporating both the **Dynamic Difficulty Adjustment (DAA)** and the **Emergency Difficulty Adjustment (EDA)**. It also explains the relationship between **difficulty** and **target**, how difficulty is stored in blocks, how it is measured (including bdiff vs. pdiff), and references various related topics such as the [[Genesis_block|Genesis Block]], [[Mining_pool|Mining pools]], etc.

---

## 1. What is Difficulty?

**Difficulty** is a measure of how hard it is to find a hash that is below a given **[[Target|target]]**.  

- When a miner hashes a block header, the resulting **256-bit** number must be **lower** than the current block’s target.
- A **lower target** means that a qualifying hash is harder to find, implying a **higher difficulty**.
- **Difficulty** answers the question: “How many times more difficult is it to mine a block now than it was to mine the [[Genesis_block|Genesis Block]]?”

### Difficulty vs. Target

- **Difficulty** and **target** have an **inverse relationship**:
  - Higher difficulty → Lower target
  - Lower difficulty → Higher target
- A **difficulty of 1** corresponds to the highest possible target (i.e., “easiest” mining). This was the difficulty for the [[Genesis_block|Genesis Block]].

---

## 2. How is the Difficulty Target Calculated in BSV?

Bitcoin SV employs two main methods to keep block production around **one block every 10 minutes**:

1. **Dynamic Difficulty Adjustment (DAA)**: Adjusts every 2,016 blocks (~2 weeks).
2. **Emergency Difficulty Adjustment (EDA)**: Adjusts after every block.

These two mechanisms ensure both **long-term stability** and **short-term responsiveness** to changes in total hash power.

---

### 2.1 Dynamic Difficulty Adjustment (DAA)

1. **Frequency**: Every **2,016 blocks** (about 2 weeks, assuming 10 minutes per block).  
2. **Purpose**: To **stabilize** the network difficulty over longer periods so the average block time stays near 10 minutes.  
3. **Formula**:

   $$
   \text{New Target}_{\text{DAA}} 
   = \text{Old Target} \times 
     \frac{\text{Actual Time Taken}}{\text{Expected Time}}
   $$

   - **New Target**\(_{DAA}\): Difficulty target for the next 2,016 blocks.
   - **Old Target**: Difficulty target used for the previous 2,016-block period.
   - **Actual Time Taken**: The time (in seconds) it took to find the last 2,016 blocks.
   - **Expected Time**: \( 2,016 \times 10 \,\text{minutes} = 120{,}960 \,\text{seconds} \).

4. **Adjustment Limits** (BSV & BCH):  
   - **Max Increase per Adjustment**: up to **100%** of the current difficulty.  
   - **Max Decrease per Adjustment**: up to **50%** of the current difficulty.

   > **Note**: The original Bitcoin Core (BTC) implementation allows up to **400%** increase and **75%** decrease per 2,016-block period.

---

### 2.2 Emergency Difficulty Adjustment (EDA)

1. **Frequency**: After **every single block**.  
2. **Purpose**: To **respond quickly** to short-term fluctuations in hash power so that blocks keep being found close to every 10 minutes, even if miners come and go rapidly.  
3. **Formula**:

   $$
   \text{New Target}_{\text{EDA}} 
   = \text{Current Target} \times 
     \frac{\text{Actual Block Time}}{\text{Expected Block Time}}
   $$

   - **New Target**\(_{EDA}\): The difficulty target for the **next** block.
   - **Current Target**: The difficulty target of the **most recent** block.
   - **Actual Block Time**: The time (in seconds) it took to find the **most recent** block.
   - **Expected Block Time**: \(10 \,\text{minutes} = 600 \,\text{seconds}\).

By combining **DAA** (long-term) and **EDA** (block-by-block), Bitcoin SV adapts smoothly to any sudden or gradual changes in overall hash rate.

---

## 3. How Often Does the Network Difficulty Change?

- **With DAA**: Automatically every **2,016 blocks** (~2 weeks).
- **With EDA**: Potentially **every block**.

Thus, BSV’s difficulty can adjust frequently, ensuring mining remains viable and block intervals remain consistent.

---

## 4. How is Difficulty Stored in Blocks?

Each Bitcoin SV block header contains a compact representation of the target known as **[[Block_hashing_algorithm|Bits]]** (often called [[nBits]]). From [[Bits]], you can derive the full 256-bit target using a set formula.

For example, if the block header’s `Bits` is `0x1b0404cb`, the target expands to:

0x0404cb * 2^(8 * (0x1b - 3)) = 0x00000000000404CB000000000000000000000000000000000000000000000000


- This corresponds to **bdiff = 1**.  
- Meanwhile, pool miners often use a looser target for “pool diff 1”:

0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF

Therefore, if your block’s [[nBits]] yields:
current_target = 0x00000000000404CB000000000000000000000000000000000000000000000000

> **Signed Format Note**: `0x0404cb` is treated as a signed value, and certain bounds exist for valid `Bits`. The maximum legal value for this three-byte field is `0x7fffff`. Larger values require shifting the exponent.


Then:

- **bdiff** ≈

  $$
  \frac{0x00000000FFFF0000000000000000000000000000000000000000000000000000}
       {0x00000000000404CB000000000000000000000000000000000000000000000000}
  $$

- **pdiff** ≈

  $$
  \frac{0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF}
       {0x00000000000404CB000000000000000000000000000000000000000000000000}
  $$

These can be computed exactly with arbitrary-precision arithmetic (e.g., using Python’s `decimal` or C++ big-integer libraries).

---

## Summary

1. **DAA** adjusts difficulty every **2,016 blocks** (~2 weeks), limiting large swings and keeping the long-term block interval near 10 minutes.  
2. **EDA** recalculates difficulty after **every block**, making rapid changes if miners suddenly join or leave.  
3. **Difficulty** is an inverse measure to the **[[Target|target]]**; a lower target means higher difficulty.  
4. Each block stores its target in a compact form (`Bits`), which expands to a 256-bit target.  
5. **Difficulty** is typically expressed as either **bdiff** or **pdiff**, depending on the base target used.  
6. **Network Hash Rate** can be estimated from difficulty, showing how much computational power is mining on the chain.  
7. **Limits on difficulty changes** in BSV/BCH: up to +100% or -50% each 2,016-block period.  

Together, these mechanisms ensure **Bitcoin SV** remains secure, stable, and capable of adapting to both short-term and long-term shifts in mining power.

---

## See Also
- [[Target|Target]]
- [[Mining_pool|Mining Pools]]
- [[Genesis_block|Genesis Block]]

---

### Attribution

This content is based on material originally sourced from  
[en.bitcoin.it/wiki/Difficulty](https://en.bitcoin.it/wiki/Difficulty)  
and is licensed under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/).  
It has been extensively revised and updated to reflect **Bitcoin SV** specifics.




