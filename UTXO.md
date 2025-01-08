# UTXO (Unspent Transaction Output)

The **UTXO** (Unspent Transaction Output), also referred to as a [[UTXO]], is a foundational concept in [[Electronic Cash Systems]] like [[Bitcoin]]. UTXOs serve as the backbone of the [[UTXO Model]] and represent discrete, indivisible units of value that can only be spent by satisfying specific conditions defined in their [[lockScript]].

## UTXOs as Instruments in an Electronic Cash System

A UTXO functions like a digital equivalent of a coin or banknote in an [[Electronic Cash System]]. Unlike physical currency, where denominations such as $10 or $1 exist, Bitcoin creates unique "digital bills" for exact amounts of [[Satoshis]]. Each UTXO is cryptographically secure and can only be spent by someone who has the specific secret information necessary to unlock it via an [[unlockScript]].

### Characteristics of a UTXO
- **Secure and Unique**: A UTXO is cryptographically locked with conditions defined in its [[lockScript]], ensuring only authorized spenders can use it.
- **Condition-Based Spending**: UTXOs can include programmable conditions, such as:
  - Completion of computational tasks or challenges.
  - Provision of a calculatable result, like solving a [[hash puzzle]].
  - Other conditional requirements specified in the lockScript.

## Structure of a UTXO

A UTXO is identified and referenced by:
1. **Transaction ID** ([[TXID]]): The unique identifier of the transaction that created the UTXO.
2. **Output Index** ([[VOUT]]): The index indicating which output in a transaction it corresponds to.
3. [[lockScript]]: The script defining the conditions required to spend the UTXO.

When spending a UTXO, an** [[unlockScript]] is created and broadcast to the [[core node network]] to prove that the spending conditions have been satisfied.

## Distributed Processing and Scalability

UTXOs enable efficient and distributed processing in the [[Bitcoin Network]]:
- **Edge Validation**: Transactions can be validated [[Peer-to-Peer]] without requiring centralized intermediaries.
- **Broadcast Mechanism**: Once validated locally, transactions are broadcast to [[nodes]] in the network.
- [[First-Seen Rule]]: Ensures that only the first valid transaction spending a specific UTXO is accepted, preventing [[double spending]].

This architecture supports unbounded scalability. Unlike [[Account-Based Models]], which require global state synchronization, the UTXO model allows for massive parallelism and efficient [[transaction validation]].

## Advantages of the UTXO Model

1. **Atomic Units of Value**: UTXOs are indivisible units, simplifying validation and transfer.
2. **Programmability**: Allows for advanced use cases by embedding conditions in the [[lockScript]].
3. **Privacy**: UTXOs are not tied to identities, offering a degree of [[privacy]] superior to account-based models.
4. **Scalability**: Distributed validation ensures the system can handle increasing transaction volumes efficiently.

## Tags
- #concept  
- #utxo  
- #bitcoin-architecture  
- #transaction-validation  
- #scalability  
- #cryptographic-primitives  
- #electronic-cash  














