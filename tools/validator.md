# validator.md  
*Structure Language Protocol (SLP) — Validator Specification*

---

## 1. Purpose

The SLP Validator performs **structural correctness checks** on SLP documents.  
It ensures that a document is:

- syntactically valid  
- grammatically valid  
- structurally coherent  
- semantically well‑formed  
- free of illegal constructs  
- ready for interpretation  

The validator is the **gatekeeper** of the SLP toolchain: nothing proceeds to the interpreter unless it passes validation.

---

## 2. Core Principles

The validator follows six principles:

1. **Strictness**  
   Only fully valid SLP documents pass. No silent corrections.

2. **Determinism**  
   Same input → same validation result across all platforms.

3. **Completeness**  
   All structural rules are enforced.

4. **Zero Mutation**  
   Validator never modifies the document.

5. **Clear Diagnostics**  
   Errors include rule references, line numbers, and actionable messages.

6. **Machine‑Readable Output**  
   All results can be emitted as JSON for toolchain integration.

---

## 3. Validation Pipeline

Validation occurs in four stages:

1. **Lexical Validation**  
   Tokenization and token‑level correctness.

2. **Syntax Validation**  
   Structural syntax rules (delimiters, blocks, indentation).

3. **Grammar Validation**  
   Grammar productions and allowed constructs.

4. **Semantic Validation**  
   Structural meaning: node existence, attribute placement, relation legality.

If any stage fails, validation stops and returns an error.

---

## 4. Lexical Validation

Checks include:

- valid identifiers  
- valid attribute keys  
- valid numeric formats  
- valid relation operators  
- no illegal characters  
- no unterminated strings  

Examples of lexical errors:

- `Node A` (space in identifier)  
- `dimension: 3.5.2` (invalid number)  
- `A --> B` (invalid operator)  

---

## 5. Syntax Validation

Checks include:

- block delimiters `{` `}`  
- indentation consistency  
- attribute syntax (`key: value`)  
- relation syntax (`A -> B`)  
- no relations inside node blocks  
- no attributes at top level  

Examples of syntax errors:

- mismatched braces  
- inconsistent indentation  
- `tension = 0.5` (invalid delimiter)  

---

## 6. Grammar Validation

Checks include:

- valid node forms  
- valid relation forms  
- valid block structure  
- valid attribute placement  
- valid closure/dimension grammar  
- no chained relations  
- no multi‑target relations  

Examples of grammar errors:

- `NodeA()` (empty metadata)  
- `A -> B -> C` (chaining illegal)  
- `NodeA { A -> B }` (relation inside node block)  

---

## 7. Semantic Validation

Semantic validation ensures the document is **structurally meaningful**.

Checks include:

### 7.1 Node Existence
All relation endpoints must exist.

### 7.2 Attribute Ownership
Attributes must attach only to:

- nodes  
- relations  

### 7.3 Block Semantics
Blocks must:

- have names  
- form a tree  
- not contain illegal constructs  

### 7.4 Dimension Semantics
Dimensions must be:

- integers  
- non‑negative  
- consistent with grammar  

### 7.5 Closure Semantics
Closure values must be:

- valid closure states  
- valid transitions  

### 7.6 Relation Semantics
Relations must:

- reference valid nodes  
- use valid types  
- follow directionality rules  

---

## 8. Validation Output

### 8.1 Success Output
VALID

With JSON:


{ "status": "valid", "errors": [] }

### 8.2 Error Output


ERROR <code>: <message> (line X, column Y)

With JSON:


{ "status": "invalid", "errors": [ { "code": "<error_code>", "message": "<description>", "line": X, "column": Y } ] }

---

## 9. Error Codes

Common validator error codes:

- `LEXICAL_ERROR`  
- `SYNTAX_ERROR`  
- `GRAMMAR_ERROR`  
- `SEMANTIC_ERROR`  
- `UNKNOWN_ATTRIBUTE`  
- `INVALID_RELATION`  
- `INVALID_BLOCK`  
- `INVALID_DIMENSION`  
- `INVALID_CLOSURE`  
- `ILLEGAL_PLACEMENT`  

---

## 10. Examples

### 10.1 Valid Document

Input:


BlockA { NodeA NodeB NodeA -> NodeB }

Output:


VALID

### 10.2 Invalid Document

Input:


NodeA { A -> B }

Output:


ERROR GRAMMAR_ERROR: Relation cannot appear inside node block (line 2, column 5)

---

## 11. Integration With Toolchain

The validator integrates with:

- **CLI** (`slp validate`)  
- **Formatter** (pre‑format validation)  
- **Linter** (post‑validation semantic checks)  
- **Interpreter** (requires validated input)  

Validator is the **first structural checkpoint** in the SLP pipeline.

---

## 12. Summary

The SLP Validator:

- enforces lexical, syntactic, grammatical, and semantic correctness  
- ensures structural integrity  
- prevents invalid documents from entering the interpreter  
- provides deterministic, machine‑readable diagnostics  
- forms the backbone of the SLP toolchain  

It is the **structural correctness engine** of the protocol.

