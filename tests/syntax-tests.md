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
