# syntax-tests.md  
*Structure Language Protocol (SLP) — Syntax Test Suite*

---

## 1. Purpose

Syntax tests verify that SLP source text conforms to the **structural syntax rules** defined in:

- `syntax/structural-syntax.md`
- `syntax/dimensional-syntax.md`
- `syntax/closure-syntax.md`
- `syntax/tension-syntax.md`
- `syntax/subject-syntax.md`
- `syntax/interoperability-syntax.md`

These tests ensure that:

- tokens are valid  
- delimiters are correct  
- block structure is well‑formed  
- indentation rules are respected  
- no illegal constructs appear  

Syntax tests run **before** grammar, interpreter, or runtime tests.

---

## 2. Test Categories

Syntax tests are grouped into:

1. **Token Tests**  
2. **Delimiter Tests**  
3. **Block Structure Tests**  
4. **Attribute Syntax Tests**  
5. **Closure Syntax Tests**  
6. **Dimension Syntax Tests**  
7. **Error Case Tests**

Each category includes valid and invalid examples.

---

## 3. Token Tests

### 3.1 Valid Tokens


NodeA node_b RELATION dimension:3 closure:open

Expected: **pass**

### 3.2 Invalid Tokens


Node A        # spaces not allowed node-1        # hyphens illegal unless specified 3dimension    # cannot start with number

Expected: **syntax error**

---

## 4. Delimiter Tests

### 4.1 Valid Delimiters


A -> B A <-> B A -(supports)-> B

Expected: **pass**

### 4.2 Invalid Delimiters


A --> B          # double arrow not allowed A - supports -> B A <--> B         # illegal bidirectional form

Expected: **syntax error**

---

## 5. Block Structure Tests

### 5.1 Valid Block


BlockA { NodeA NodeB }

Expected: **pass**

### 5.2 Invalid Block


BlockA { NodeA NodeB        # inconsistent indentation }

Expected: **syntax error**

---

## 6. Attribute Syntax Tests

### 6.1 Valid Attributes


NodeA { tension: 0.8 polarity: +1 load: 12 }

Expected: **pass**

### 6.2 Invalid Attributes


NodeA { tension = 0.8     # wrong delimiter polarity: ++1     # invalid polarity }

Expected: **syntax error**

---

## 7. Closure Syntax Tests

### 7.1 Valid Closure Syntax


NodeA { closure: open }

Expected: **pass**

### 7.2 Invalid Closure Syntax


NodeA { closure: opened }

Expected: **syntax error**

---

## 8. Dimension Syntax Tests

### 8.1 Valid Dimension Syntax


NodeA { dimension: 3 }

Expected: **pass**

### 8.2 Invalid Dimension Syntax


NodeA { dimension: -1      # negative dimension illegal }

Expected: **syntax error**

---

## 9. Error Case Tests

These tests ensure the syntax validator rejects malformed input.

### 9.1 Mixed Syntax Error


NodeA { tension: 0.5 A -> B }

Expected: **syntax error**  
Reason: relations cannot appear inside node blocks.

### 9.2 Unterminated Block


BlockA { NodeA

Expected: **syntax error**

### 9.3 Unknown Keyword


NodeA { flavor: spicy }

Expected: **syntax error**

---

## 10. Summary

This test suite verifies:

- token validity  
- delimiter correctness  
- block structure  
- attribute syntax  
- closure and dimension syntax  
- rejection of malformed constructs  

Syntax tests ensure that only **well‑formed SLP documents** proceed to grammar and interpreter stages.



