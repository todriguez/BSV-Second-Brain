The **Alt Stack** (alternative stack) is a key concept in **Stack-Based Programming Languages** [[Stack-Based Programming Languages]], particularly within the domain of **Bitcoin Script** [[Bitcoin Script]].

## Concept

The Alt Stack is a secondary data structure in the Bitcoin Virtual Machine (VM) that operates alongside the main stack. It provides temporary storage and enables additional flexibility during script execution and transaction validation. By allowing data to be moved between the main stack and the Alt Stack, it facilitates the creation of more complex script patterns.

The Alt Stack is distinct from the main stack, maintaining its own separate data and operations. Specific opcodes, such as `OP_TOALTSTACK` and `OP_FROMALTSTACK`, are used to transfer items between the two stacks. This functionality is crucial for managing intermediate computations and preserving the integrity of the main stack during certain operations.

## Role and Usage

The Alt Stack complements the main stack by enabling smoother execution of complex scripts. Specific opcodes allow interactions between the two stacks:

- `OP_TOALTSTACK`: Transfers the top item from the main stack to the Alt Stack.
- `OP_FROMALTSTACK`: Transfers the top item from the Alt Stack back to the main stack.
- `OP_2DROP`: Drops the top two items from the Alt Stack.

Items on the Alt Stack persist even after the script execution ends, which can be critical for retaining intermediate states during transaction validation.

## Tags
- #concept  
- #bitcoin-vm  
- #stack-operations  
