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
