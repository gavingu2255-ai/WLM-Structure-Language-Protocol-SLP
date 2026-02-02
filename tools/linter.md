# linter.md  
*Structure Language Protocol (SLP) — Linter Specification*

---

## 1. Purpose

The SLP Linter performs **structural quality checks** that go beyond strict correctness.  
Where the validator enforces *validity*, the linter enforces:

- clarity  
- consistency  
- maintainability  
- best practices  
- structural hygiene  

The linter never changes semantics.  
It only identifies (and optionally fixes) issues that degrade readability, interoperability, or long‑term structural stability.

---

## 2. Core Principles

The linter follows seven principles:

1. **Non‑Destructive**  
   Linter suggestions never alter meaning.

2. **Deterministic**  
   Same input → same lint report across all platforms.

3. **Best‑Practice Enforcement**  
   Encourages canonical SLP style and structure.

4. **Semantic Awareness**  
   Linter understands nodes, relations, blocks, attributes, and propagation semantics.

5. **Minimal False Positives**  
   Only flags issues with clear structural justification.

6. **Actionable Output**  
   Every lint message includes a fix suggestion.

7. **Machine‑Readable**  
   JSON output supported for toolchain integration.

---

## 3. Lint Categories

The linter checks for:

1. **Structural Hygiene Issues**  
2. **Redundant Constructs**  
3. **Ambiguous Constructs**  
4. **Style Consistency Issues**  
5. **Best‑Practice Violations**  
6. **Interoperability Risks**  
7. **Deprecated Syntax or Grammar**

Each category is described below.

---

## 4. Structural Hygiene Checks

### 4.1 Unused Nodes

Flags nodes that never appear in:

- relations  
- blocks  
- attribute references  

Example:
NodeA NodeB NodeA -> NodeB

Linter flags: `NodeB` is used; `NodeA` is used; no issue.

But:


NodeA NodeB

Linter flags: `NodeB` unused.

---

### 4.2 Unreachable Blocks

Flags blocks that are never referenced or nested meaningfully.

### 4.3 Orphan Attributes

Attributes attached to nothing (should never occur after validation).

---

## 5. Redundant Construct Checks

### 5.1 Duplicate Node Declarations

Example:


NodeA NodeA

Linter:  
“Duplicate declaration of NodeA; merge recommended.”

### 5.2 Redundant Attributes

Example:


NodeA { tension: 0.5 tension: 0.5 }

Linter:  
“Redundant attribute; remove duplicate.”

### 5.3 Redundant Relations

Example:


A -> B A -> B

Linter:  
“Duplicate relation; remove one.”

---

## 6. Ambiguous Construct Checks

### 6.1 Ambiguous Relation Types

Example:


A -(supports)-> B A -(helps)-> B

Linter:  
“Multiple relation types between same nodes; consider consolidation.”

### 6.2 Ambiguous Block Nesting

Flags blocks that could be flattened without semantic loss.

### 6.3 Ambiguous Attribute Placement

Example:


NodeA(type:entity) { type: entity }

Linter:  
“Attribute duplicated across inline and block forms.”

---

## 7. Style Consistency Checks

### 7.1 Indentation Consistency

Ensures:

- 4‑space indentation  
- no tabs  
- no mixed indentation  

### 7.2 Attribute Ordering

Ensures canonical order:

1. type  
2. dimension  
3. closure  
4. tension  
5. polarity  
6. load  
7. alphabetical remainder  

### 7.3 Relation Spacing

Ensures:

- `A -> B`  
- not `A->B` or `A  ->   B`

### 7.4 Block Formatting

Ensures:


BlockA { ... }

Never:


BlockA{ ... }

---

## 8. Best‑Practice Checks

### 8.1 Missing Attributes

Flags nodes that likely need attributes based on context.

Example:


A -> B

If B has no attributes and A has many, linter may suggest:

“NodeB has no attributes; verify this is intentional.”

### 8.2 Missing Dimensions in Dimensional Graphs

If most nodes have dimensions but one does not, linter flags it.

### 8.3 Missing Closure in Closure‑Driven Graphs

If closure is used inconsistently, linter warns.

---

## 9. Interoperability Risk Checks

### 9.1 Non‑Canonical Relation Forms

Example:


A --> B

Linter:  
“Non‑canonical arrow; use `A -> B`.”

### 9.2 Deprecated Syntax

Flags constructs removed from the latest grammar.

### 9.3 Non‑Deterministic Ordering

Flags:

- unordered blocks  
- unordered relations  
- unordered attributes  

---

## 10. Linter Output Format

### 10.1 Human‑Readable Output


[LINT] WARNING: Duplicate node declaration (NodeA) at line 3 [LINT] SUGGESTION: Remove redundant declaration

### 10.2 JSON Output


{ "status": "linted", "issues": [ { "code": "DUPLICATE_NODE", "message": "Duplicate node declaration", "line": 3, "suggestion": "Remove redundant declaration" } ] }

---

## 11. Auto‑Fix Mode

The linter supports safe auto‑fixing:


slp lint file.slp --fix

Auto‑fix applies only:

- redundant removal  
- canonical ordering  
- spacing fixes  
- indentation fixes  

Auto‑fix **never**:

- changes semantics  
- rewrites relations  
- alters attributes  
- restructures blocks  

---

## 12. Integration With Toolchain

The linter integrates with:

- **CLI** (`slp lint`)  
- **Formatter** (post‑format linting)  
- **Validator** (pre‑lint validation)  
- **Interpreter** (optional pre‑interpret linting)  

The linter is the **structural hygiene layer** of the SLP ecosystem.

---

## 13. Summary

The SLP Linter:

- enforces structural hygiene  
- detects redundancy and ambiguity  
- ensures style consistency  
- flags interoperability risks  
- supports safe auto‑fixing  
- preserves semantics  
- produces deterministic, actionable reports  

It is the **quality assurance engine** of the SLP toolchain.


