# interpreter-tests.md  
*Structure Language Protocol (SLP) — Interpreter Test Suite*

---

## 1. Purpose

Interpreter tests verify that the SLP interpreter:

- accepts syntax‑valid and grammar‑valid documents  
- produces a correct **Resolved Structural Graph (RSG)**  
- resolves blocks, nodes, relations, and attributes  
- applies default values  
- normalizes structure  
- rejects invalid constructs with clear errors  

Interpreter tests run **after grammar tests** and **before resolution and runtime tests**.

---

## 2. Test Categories

Interpreter tests are grouped into:

1. **Node Interpretation Tests**  
2. **Relation Interpretation Tests**  
3. **Block Interpretation Tests**  
4. **Attribute Interpretation Tests**  
5. **Mixed Structure Interpretation Tests**  
6. **Normalization Tests**  
7. **Error Case Tests**

Each category includes expected RSG output.

---

## 3. Node Interpretation Tests

### 3.1 Basic Node

Input:


NodeA

Expected RSG:
- NodeA created  
- default dimension = 0  
- no attributes  
- no relations  

### 3.2 Node With Type

Input:


NodeA(type:entity)

Expected RSG:
- NodeA with type = entity  

### 3.3 Node With Dimension

Input:


NodeA(dimension:3)

Expected RSG:
- NodeA with dimension = 3  

---

## 4. Relation Interpretation Tests

### 4.1 Simple Relation

Input:


A -> B

Expected RSG:
- Node A  
- Node B  
- Relation A→B (type: directional)  

### 4.2 Typed Relation

Input:


A -(supports)-> B

Expected RSG:
- Relation type = supports  
- Direction = A→B  

### 4.3 Bidirectional Relation

Input:


A <-> B

Expected RSG:
- Two directional relations: A→B and B→A  
- Relation type = bidirectional  

---

## 5. Block Interpretation Tests

### 5.1 Basic Block

Input:


BlockA { NodeA NodeB }

Expected RSG:
- BlockA created  
- NodeA and NodeB assigned to BlockA  

### 5.2 Nested Blocks

Input:


BlockA { BlockB { NodeA } }

Expected RSG:
- Block hierarchy: BlockA → BlockB  
- NodeA assigned to BlockB  

---

## 6. Attribute Interpretation Tests

### 6.1 Node Attributes

Input:


NodeA { tension: 0.5 polarity: +1 }

Expected RSG:
- NodeA with attributes:  
  - tension = 0.5  
  - polarity = +1  

### 6.2 Relation Attributes

Input:


A -> B { load: 12 }

Expected RSG:
- Relation A→B with load = 12  

---

## 7. Mixed Structure Interpretation Tests

### 7.1 Node + Relation + Attributes

Input:


BlockA { NodeA(type:entity) NodeB(dimension:2) NodeA -> NodeB NodeB { tension: 0.8 } }

Expected RSG:
- BlockA contains NodeA, NodeB, and relation A→B  
- NodeA type = entity  
- NodeB dimension = 2, tension = 0.8  

### 7.2 Multi‑Block Mixed Example

Input:


BlockA { NodeA BlockB { NodeB NodeA -> NodeB } }

Expected RSG:
- BlockA contains NodeA and BlockB  
- BlockB contains NodeB and relation A→B  

---

## 8. Normalization Tests

### 8.1 Duplicate Node Declaration

Input:


NodeA NodeA

Expected RSG:
- Single NodeA  
- Interpreter merges declarations  

### 8.2 Attribute Merge

Input:


NodeA { tension: 0.5 } NodeA { polarity: +1 }

Expected RSG:
- NodeA with both attributes  
- No duplication  

### 8.3 Relation Normalization

Input:


A <-> B

Expected RSG:
- Two directional relations  
- Both normalized to standard relation form  

---

## 9. Error Case Tests

### 9.1 Unknown Attribute

Input:


NodeA { flavor: spicy }

Expected: **interpreter error**  
Reason: unknown attribute.

### 9.2 Relation With Missing Node

Input:


A -> B C

Expected: **interpreter error**  
Reason: Node B referenced before declaration is allowed,  
but Node A or B must be valid identifiers.  
If malformed, interpreter rejects.

### 9.3 Block Misplacement

Input:


NodeA { NodeB }

Expected: **interpreter error**  
Reason: blocks must have names.

### 9.4 Attribute Outside Node/Relation

Input:


tension: 0.5 NodeA

Expected: **interpreter error**

---

## 10. Summary

This test suite verifies that the interpreter:

- constructs correct RSGs  
- resolves nodes, relations, blocks, and attributes  
- applies normalization rules  
- merges declarations  
- rejects invalid constructs  
- produces deterministic output  

Interpreter tests ensure that only **fully resolved structural graphs** proceed to the resolution and runtime stages.



