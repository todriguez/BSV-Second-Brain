A **51% attack** is a theoretical attack scenario in which a malicious node gains control of more than 50% of the network's [[Hash Power]]. This majority allows the attacker to manipulate the blockchain by producing blocks that may include double spends, invalid transactions, or violations of established consensus rules. 

## Characteristics of a 51% Attack

1. **Significant Resource Requirement**:  
   Such an attack requires substantial hash power, incurring high costs in terms of energy, hardware, and infrastructure.  
   - The attacker must dedicate these resources to building an alternative chain that overtakes the longest [[Honest Chain]].

2. **Immutable Evidence Trail**:  
   Any attempted attack leaves an immutable, forensic evidence trail due to the [[Blockchain]]'s transparency.  
   - This allows for post-attack analysis and attribution to the attacking node or entity.

3. **Honest Behavior Defined by Law**:  
   Honesty within the Bitcoin [[Protocol]] is determined by adhering to the rules set forth in [[Network Access Rules]] and processing only legitimate transactions.  
   - Fraudulent transactions or protocol deviations are considered dishonest and can be prosecuted under applicable laws.

## Honest Chain and Protocol Integrity

The **longest honest chain** refers to the chain of blocks adhering to the original, unaltered protocol rules, as outlined in the [[Bitcoin Whitepaper]]. Honest nodes are defined as those that:
- Follow the protocol exactly as designed.
- Uphold the integrity of the [[Chain of Digital Signatures]].
- Reject invalid transactions and rule violations.

## Attack Dynamics

According to the [[Bitcoin Whitepaper]], even if an attacker possesses more hash power than the rest of the network combined:
1. They must extend a dishonest chain tip that includes fraudulent transactions, such as double spends.
2. Honest nodes will always prefer the longest honest chain, ensuring that resources spent by the attacker are wasted unless they can sustain the attack indefinitely.
3. The economic incentives discourage such attacks, as the costs of execution far outweigh any potential rewards.

### BTC as a Case Study in Protocol Dishonesty
The [[SegWit]] protocol alteration in BTC introduced fundamental changes to Bitcoin's [[Set-in-Stone Protocol]], including breaking the chain of digital signatures. Honest nodes adhering to the original protocol rules rejected this change, resulting in [[BSV Blockchain]] continuing as the honest chain. From this perspective, BTC's continuation with a mutated protocol can be viewed as an ongoing 51% attack, extending a dishonest chain.

## Conclusion

A 51% attack is not merely a function of hash power dominance; it also involves violating the foundational rules of the Bitcoin protocol. While theoretically possible, such attacks are highly impractical due to their costs and the transparency of the [[Blockchain]], which leaves a forensic trail. The adherence to honesty as defined by law and protocol ensures that honest nodes prevail in maintaining the integrity of Bitcoin.

---

### See Also:
- [[Hash Power]]
- [[Longest Honest Chain]]
- [[Bitcoin Whitepaper]]
- [[Chain of Digital Signatures]]
- [[Network Access Rules]]
- [[SegWit]]
- [[BSV Blockchain]]
- [[Blockchain Forensics]]
