# glossary.md  
*Structure Language Protocol (SLP) — Glossary*

A concise, authoritative reference for all core SLP terms.  
Every definition is written to be unambiguous, implementation‑neutral, and structurally precise.

---

## A

### **Attribute**
A key–value property attached to a node or relation.  
Attributes influence resolution and runtime behavior (e.g., `tension`, `polarity`, `dimension`, `closure`).

### **Atomicity**
A runtime guarantee that updates either fully succeed or fully fail.  
No partial or inconsistent states are ever committed.

---

## B

### **Block**
A hierarchical container grouping nodes, relations, and child blocks.  
Blocks provide inheritance, scoping, and structural organization.

### **Block Inheritance**
The mechanism by which nodes and relations inside a block inherit attributes defined at the block level.

---

## C

### **Canonical Form**
The normalized, deterministic representation of an SLP document produced by the formatter.

### **Closure**
A structural state or phase of a node (e.g., `open`, `closed`, or transitions like `A -> B`).  
Resolved during the resolution phase.

### **Conflict Resolution**
The deterministic rules used to resolve contradictory attributes or propagation results.

### **Cycle**
A closed loop of relations (e.g., `A -> B -> C -> A`).  
Cycles are resolved deterministically during resolution and runtime.

---

## D

### **Dimension**
A non‑negative integer representing a node’s structural depth or degree.  
Dimensions propagate and align through relations.

### **Determinism**
The guarantee that identical input always produces identical output across all interpreters and runtimes.

---

## E

### **Event**
A runtime instruction such as `set_attribute`, `tick`, or `run_until_stable`.  
Events drive structural evolution.

### **Event Loop**
The runtime subsystem that processes events in FIFO order with snapshot isolation.

---

## F

### **FRSG (Fully Resolved Structural Graph)**
The graph produced after resolution.  
All inheritance, propagation, closure transitions, and dimensional alignment have been applied.

### **Formatter**
A tool that rewrites SLP documents into canonical form without changing semantics.

---

## G

### **Grammar**
The formal rules defining legal SLP constructs and their allowed combinations.

### **Graph**
The structural representation consisting of nodes, relations, blocks, and attributes.

---

## I

### **Interpreter**
The subsystem that converts SLP text into an RSG (Resolved Structural Graph).

### **Inheritance**
The process by which attributes flow from blocks to nodes and relations.

### **Interoperability**
The requirement that all SLP implementations behave identically and produce identical results.

---

## L

### **Linter**
A tool that detects structural hygiene issues, redundancies, ambiguities, and style inconsistencies.

---

## N

### **Node**
A structural entity representing an object, concept, or unit.  
Nodes may have attributes, dimensions, and closure states.

### **Normalization**
Interpreter step that merges duplicate declarations, orders attributes, and standardizes structure.

---

## P

### **Propagation**
The process by which attributes flow along relations during resolution and runtime.

### **Protocol**
A deterministic, cross‑implementation standard defining syntax, grammar, interpretation, resolution, and runtime behavior.

---

## R

### **Relation**
A directed or bidirectional connection between nodes (e.g., `A -> B`, `A <-> B`, `A -(type)-> B`).

### **Resolution**
The phase that transforms an RSG into an FRSG by applying propagation, inheritance, closure transitions, and conflict resolution.

### **RSG (Resolved Structural Graph)**
The graph produced by the interpreter before resolution.  
Normalized but not yet executed.

### **Runtime**
The execution engine that processes events, applies updates, and maintains structural consistency.

---

## S

### **Semantic Validation**
Validation step ensuring the document is structurally meaningful (e.g., nodes exist, attributes are legal).

### **Snapshot Isolation**
Runtime guarantee that each event sees a stable, consistent view of the graph.

### **Syntax**
The surface form of SLP: tokens, delimiters, indentation, and block structure.

---

## T

### **Tension**
A numeric attribute representing structural load or pressure.  
Propagates through relations.

### **Toolchain**
The suite of tools: formatter, validator, linter, CLI, and interoperability tests.

---

## V

### **Validator**
A tool that checks lexical, syntactic, grammatical, and semantic correctness.

---

## W

### **WLM (World‑Level Memory) Flags**
Runtime status indicators such as `BUFFER_STABLE`, `CONSISTENCY_OK`, and `INTEGRITY_NORMALIZED`.

---

## Summary

This glossary defines the core vocabulary of SLP:

- syntax → grammar → interpretation → resolution → runtime  
- nodes, relations, blocks, attributes  
- determinism, propagation, inheritance, closure, dimension  
- toolchain and interoperability concepts  

It serves as the authoritative reference for all structural terms used throughout the SLP specification and documentation.
