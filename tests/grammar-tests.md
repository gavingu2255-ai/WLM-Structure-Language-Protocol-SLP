# grammar-tests.md  
*Structure Language Protocol (SLP) — Grammar Test Suite*

---

## 1. Purpose

Grammar tests verify that SLP documents which pass **syntax validation** also conform to the **formal grammar rules** defined in:

- `grammar/core-grammar.md`
- `grammar/node-grammar.md`
- `grammar/relation-grammar.md`
- `grammar/block-grammar.md`
- `grammar/attribute-grammar.md`
- `grammar/closure-grammar.md`
- `grammar/dimension-grammar.md`

These tests ensure that:

- constructs appear in legal positions  
- grammar productions match expected forms  
- blocks contain only allowed statements  
- relations follow valid grammar patterns  
- attributes attach only to valid owners  
- ordering rules are respected  

Grammar tests run **after syntax tests** and **before interpreter tests**.

---

## 2. Test Categories

Grammar tests are grouped into:

1. **Node Grammar Tests**  
2. **Relation Grammar Tests**  
3. **Block Grammar Tests**  
4. **Attribute Grammar Tests**  
5. **Closure Grammar Tests**  
6. **Dimension Grammar Tests**  
7. **Mixed Grammar Tests**  
8. **Invalid Grammar Tests**

Each category includes valid and invalid examples.

---

## 3. Node Grammar Tests

### 3.1 Valid Node Forms


NodeA NodeB(type:entity) NodeC(dimension:3)

Expected: **grammar pass**

### 3.2 Invalid Node Forms


NodeA() NodeB(type:) NodeC(dimension:high)

Expected: **grammar error**

Reason: empty parentheses, missing values, invalid dimension type.

---

## 4. Relation Grammar Tests

### 4.1 Valid Relation Forms


A -> B A <-> B A -(supports)-> B A -(corrects)-> B

Expected: **grammar pass**

### 4.2 Invalid Relation Forms


A -> B -> C        # chained relations illegal A -(unknown)-> B   # unknown relation type A <-> B <-> C      # multi-target illegal

Expected: **grammar error**

---

## 5. Block Grammar Tests

### 5.1 Valid Block Forms


BlockA { NodeA A -> B }

Expected: **grammar pass**

### 5.2 Invalid Block Forms


BlockA { dimension: 3      # attributes cannot appear at block root NodeA }

Expected: **grammar error**

---

## 6. Attribute Grammar Tests

### 6.1 Valid Attribute Placement


NodeA { tension: 0.5 polarity: +1 }

Expected: **grammar pass**

### 6.2 Invalid Attribute Placement


A -> B { tension: 0.5 }

Expected: **grammar error**

Reason: relations cannot contain blocks.

---

## 7. Closure Grammar Tests

### 7.1 Valid Closure Forms


NodeA { closure: open }

Expected: **grammar pass**

### 7.2 Invalid Closure Forms


NodeA { closure: open -> closed }

Expected: **grammar error**

Reason: closure transitions belong to runtime, not grammar.

---

## 8. Dimension Grammar Tests

### 8.1 Valid Dimension Forms


NodeA(dimension:2) NodeB { dimension: 4 }

Expected: **grammar pass**

### 8.2 Invalid Dimension Forms


NodeA(dimension:2.5) NodeB(dimension:-1)

Expected: **grammar error**

Reason: dimensions must be non‑negative integers.

---

## 9. Mixed Grammar Tests

### 9.1 Valid Mixed Example


BlockA { NodeA(type:entity) NodeB(dimension:3) NodeA -> NodeB }

Expected: **grammar pass**

### 9.2 Invalid Mixed Example


BlockA { NodeA NodeB tension: 0.5      # illegal at block level }

Expected: **grammar error**

---

## 10. Invalid Grammar Tests

These ensure the grammar rejects structurally illegal constructs.

### 10.1 Attribute Before Node


tension: 0.5 NodeA

Expected: **grammar error**

### 10.2 Relation Inside Node Block


NodeA { A -> B }

Expected: **grammar error**

### 10.3 Node Inside Attribute


NodeA { tension: NodeB }

Expected: **grammar error**

---

## 11. Summary

This test suite verifies:

- node grammar  
- relation grammar  
- block grammar  
- attribute grammar  
- closure and dimension grammar  
- rejection of illegal structural forms  

Grammar tests ensure that only **structurally valid SLP documents** proceed to interpreter evaluation.



