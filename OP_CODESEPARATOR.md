# [[OP_CODESEPARATOR]]

**`OP_CODESEPARATOR`** is an opcode in the [[Bitcoin Script]] system. It specifies a point in the script that affects how signatures are hashed and verified. This opcode is actively used in [[BSV Blockchain]] for defining boundaries in scripts, particularly for [[Smart Contract]] and [[Token Representations]].

---

## Purpose of OP_CODESEPARATOR

`OP_CODESEPARATOR` allows specific sections of a script to be excluded from the hash used in signature verification. When `OP_CHECKSIG` or `OP_CHECKSIGVERIFY` is executed, only the portion of the script from the most recent `OP_CODESEPARATOR` to the end is included in the hash calculation.

This functionality enables:

- Modular script design.  
- The ability to delineate data payloads within a script.  
- Flexible transaction designs that allow portions of a script to be reused or modified without invalidating the signature.

---

## How OP_CODESEPARATOR Works

1. **Hash Segmentation**:  
   When `OP_CHECKSIG` or `OP_CHECKSIGVERIFY` is called, the script is hashed starting from the most recent `OP_CODESEPARATOR`.  

2. **Signature Scope Control**:  
   This limits the scope of the signature to specific parts of the script, enabling the inclusion of external or dynamic data in a transaction without compromising the validity of the signature.

---

## Use Cases in BSV

### **Data Payload Management**

`OP_CODESEPARATOR` is commonly used to delineate data within scripts, ensuring clear separation between executable conditions and embedded payloads. This is particularly important in:

- **Smart Contracts**: Scripts with multiple conditions or stages.  
- **Token Standards**: Defining structured data for [[Token Representations]].  

### **Signature Flexibility**

By controlling the portions of a script that are hashed, `OP_CODESEPARATOR` allows for dynamic and reusable script components.

---

## Tags

- [[OP_CODESEPARATOR]]  
- [[Bitcoin Script]]  
- [[Smart Contract]]  
- [[Token Representations]]  
- [[Signature]]  
- [[OP_CHECKSIG]]  
- [[OP_CHECKSIGVERIFY]]  
- [[Data Payloads]]  
- [[BSV Features]]  
