# formatter.md  
*Structure Language Protocol (SLP) — Canonical Formatter Specification*

---

## 1. Purpose

The SLP Formatter produces a **canonical, deterministic textual representation** of any SLP document.  
Its goals are:

- structural clarity  
- stable round‑trips (parse → format → parse)  
- zero semantic drift  
- consistent indentation and alignment  
- predictable diffs for version control  
- interoperability across tools and runtimes  

The formatter never changes meaning — only presentation.

---

## 2. Core Principles

The formatter follows seven principles:

1. **Determinism**  
   Same input graph → same formatted output across all platforms.

2. **Idempotence**  
   Formatting an already formatted file produces no changes.

3. **Semantic Preservation**  
   Formatting never alters structure, attributes, or relations.

4. **Canonical Ordering**  
   Nodes, relations, attributes, and blocks follow a fixed order.

5. **Minimalism**  
   No decorative whitespace, no stylistic noise.

6. **Human‑Readable**  
   Clean indentation and alignment for clarity.

7. **Machine‑Friendly**  
   Output is stable for diffing, hashing, and round‑trip parsing.

---

## 3. Formatting Pipeline

The formatter operates in four stages:

1. **Parse**  
   Convert SLP text into an RSG (Resolved Structural Graph).

2. **Normalize**  
   Apply canonical ordering and structural normalization.

3. **Render**  
   Convert normalized graph back into canonical SLP text.

4. **Verify**  
   Re‑parse output to ensure round‑trip stability.

If verification fails, formatter aborts with an error.

---

## 4. Canonical Ordering Rules

### 4.1 Top‑Level Ordering

Top‑level items appear in this order:

1. Blocks  
2. Nodes  
3. Relations  

### 4.2 Block Ordering

Inside a block:

1. Child blocks (alphabetical by name)  
2. Nodes (alphabetical)  
3. Relations (alphabetical by `from`, then `to`)  
4. Node‑local attribute blocks  

### 4.3 Attribute Ordering

Attributes inside a node or relation block follow:

1. `type`  
2. `dimension`  
3. `closure`  
4. `tension`  
5. `polarity`  
6. `load`  
7. all other attributes sorted alphabetically  

### 4.4 Relation Ordering

Relations are sorted by:

1. `from` node name  
2. `to` node name  
3. relation type  

---

## 5. Indentation Rules

- Indentation uses **4 spaces** (never tabs).  
- Blocks increase indentation by one level.  
- Attributes inside a block align vertically.  
- No trailing whitespace.  
- No blank line at file start or end.

Example:
BlockA { NodeA { tension: 0.5 polarity: +1 }
NodeA -> NodeB




}

---

## 6. Spacing Rules

- Exactly **one blank line** between top‑level items.  
- No blank lines inside attribute blocks.  
- No blank lines between consecutive relations.  
- One space around arrows: `A -> B`, `A <-> B`.

---

## 7. Canonical Relation Forms

Formatter rewrites relations into canonical forms:

- `A -> B`  
- `A <-> B`  
- `A -(type)-> B`  

No alternative arrow styles are permitted.

---

## 8. Canonical Block Forms

Blocks always use:


BlockName { ... }

Rules:

- Opening brace on same line as block name.  
- Closing brace on its own line.  
- No trailing comments or inline metadata.

---

## 9. Canonical Node Forms

Nodes without attributes:


NodeA

Nodes with attributes:


NodeA { tension: 0.5 polarity: +1 }

Nodes with inline metadata (type/dimension):


NodeA(type:entity, dimension:3)

Formatter may expand inline metadata into block form if needed for clarity.

---

## 10. Canonical Attribute Forms

Attributes always use:


key: value

Rules:

- No `=`  
- No extra spaces  
- No quotes unless required by grammar  
- Numeric values normalized (e.g., `0.500` → `0.5`)  

---

## 11. Error Handling

Formatter errors include:

- `FORMAT_SYNTAX_ERROR`  
- `FORMAT_GRAMMAR_ERROR`  
- `FORMAT_NORMALIZATION_ERROR`  
- `FORMAT_ROUNDTRIP_ERROR`  

On error:

- formatter prints structured error  
- no output is produced  
- no partial formatting  

---

## 12. Examples

### 12.1 Input (messy)


BlockA{ NodeB NodeA{polarity:+1} NodeA->NodeB }

### 12.2 Output (canonical)


BlockA { NodeA { polarity: +1 }
NodeB

NodeA -> NodeB


}

---

## 13. Summary

The SLP Formatter:

- enforces canonical structure  
- ensures deterministic output  
- preserves semantics  
- supports round‑trip stability  
- integrates with validator, linter, and CLI  

It is the **presentation layer** of the SLP toolchain, ensuring every SLP document is clean, readable, and structurally consistent.

