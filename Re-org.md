# Re-Org

## Overview

A **Re-Org** (short for reorganization) occurs when the blockchain reorganizes its structure due to a longer valid chain being discovered. This happens as nodes follow the **Longest Honest Chain** rule outlined in the [[Bitcoin Whitepaper]], where the chain with the most accumulated proof of work is treated as the valid chain.

Re-orgs are a normal part of blockchain operation during [[Orphan Race|orphan races]] but can indicate malicious intent if they extend beyond a few blocks in depth.

---

## Why Re-Orgs Happen

1. **Orphan Race**:
   - Two miners may simultaneously solve a block, resulting in competing chains.
   - Nodes will temporarily follow one chain until the next block is mined, resolving the conflict by adopting the chain with the most proof of work.

2. **Malicious Re-Org**:
   - A malicious actor builds a chain in secret and releases it suddenly, attempting to replace the publicly accepted chain.
   - This type of re-org typically involves a significant depth (e.g., 6+ blocks) and may aim to double-spend funds or disrupt the network.

---

## Depth of Re-Orgs

1. **Shallow Re-Orgs**:
   - Generally occur during legitimate orphan races.
   - Typically involve 1–2 blocks.
   - Are resolved quickly without any malicious implications.

2. **Deep Re-Orgs**:
   - More than a few blocks deep.
   - Indicate potential malicious activity, such as chain tip attacks or attempts to double-spend.
   - Can disrupt network trust and require robust consensus mechanisms to mitigate.

---

## Mitigating Deep Re-Orgs

1. **Proof of Work Security**:
   - Ensuring that the chain has sufficient hash power distributed among honest miners deters malicious actors.
   - A high level of hash rate makes it computationally expensive to execute a deep re-org.

2. **Economic Disincentives**:
   - Attacking the chain would require significant investment in hardware and energy, which is likely to outweigh any potential gains.

3. **Monitoring and Alert Systems**:
   - Systems like [[Alert System]] notify nodes of unusual activity, such as large, unexpected re-orgs.

---

## Re-Orgs in Practice

- On [[BSV Blockchain]], re-orgs are rare due to its robust protocol design and hash rate security.
- They are typically resolved without affecting the integrity of transactions, as all valid transactions in the replaced chain remain valid in the new chain unless explicitly double-spent.

---

## Myths About Re-Orgs

1. **Exaggerated Threats**:
   - Re-orgs are often misunderstood as catastrophic events; in reality, shallow re-orgs are a normal and harmless part of network operations.

2. **Centralization Concerns**:
   - Some argue that deep re-orgs could centralize power; however, the economic incentives of [[Proof of Work]] and the transparency of the [[BSV Blockchain]] network discourage such behavior.

---

## Tags

#ReOrg #BlockchainSecurity #BSV #LongestHonestChain #ProofOfWork #BitcoinWhitepaper #OrphanRace #Consensus

---

## See Also

- [[Longest Honest Chain]]
- [[Proof of Work]]
- [[Orphan Race]]
- [[Alert System]]
- [[Double-Spending]]
- [[Block Header]]
