# memory-model.md  
*Structure Language Protocol (SLP) — Runtime Memory Model*

---

## 1. Purpose

The Memory Model defines **how the SLP runtime stores and manages all structural data** during execution.  
While the state model describes *what* exists, the memory model describes *how it is stored, accessed, and mutated*.

The memory model ensures:

- fast access  
- deterministic updates  
- normalized storage  
- safe propagation  
- atomic mutation  
- zero hidden state  

It is the **structural substrate** of the runtime.

---

## 2. Core Principles

The memory model follows six principles:

1. **Normalization**  
   All data is stored in normalized graph form.

2. **Index‑First Access**  
   Every lookup is O(1) or O(log n) via indices.

3. **Immutable Snapshots**  
   Execution uses read‑only snapshots for consistency.

4. **Atomic Mutation**  
   Updates apply only after full validation.

5. **No Hidden State**  
   All memory is explicit and externally observable through the API.

6. **Deterministic Layout**  
   Memory layout must be identical across implementations.

---

## 3. Memory Components

The runtime maintains five memory components:

1. **Node Memory**  
2. **Relation Memory**  
3. **Block Memory**  
4. **Attribute Memory**  
5. **Metadata Memory**

Each component is stored separately but linked through indices.

---

## 4. Node Memory

Nodes are stored in a normalized table.

### 4.1 Node Structure

Each node entry contains:

- `id`  
- `type`  
- `dimension`  
- `attributes` → attribute IDs  
- `relations_in` → relation IDs  
- `relations_out` → relation IDs  
- `block` → block ID  
- `metadata`  

### 4.2 Node Indices

Nodes are indexed by:

- ID (primary)  
- type  
- dimension  
- block  

### 4.3 Node Memory Guarantees

- Node IDs are immutable  
- Node entries cannot contain nested structures  
- All references must point to valid memory entries  

---

## 5. Relation Memory

Relations are stored in a normalized table.

### 5.1 Relation Structure

Each relation entry contains:

- `id`  
- `from` → node ID  
- `to` → node ID  
- `type`  
- `attributes` → attribute IDs  
- `metadata`  

### 5.2 Relation Indices

Relations are indexed by:

- ID (primary)  
- from → to  
- type  

### 5.3 Relation Memory Guarantees

- No relation may reference a non‑existent node  
- Bidirectional relations must be stored as two directional entries unless defined otherwise  
- Relation types must be valid  

---

## 6. Block Memory

Blocks define hierarchical structure.

### 6.1 Block Structure

Each block entry contains:

- `id`  
- `parent` → block ID  
- `children` → block IDs  
- `statements` → node/relation IDs  
- `metadata`  

### 6.2 Block Indices

Blocks are indexed by:

- ID (primary)  
- parent  
- depth  

### 6.3 Block Memory Guarantees

- Block hierarchy must form a tree  
- No cycles allowed  
- No orphan blocks  

---

## 7. Attribute Memory

Attributes include:

- tension  
- polarity  
- load  
- closure state  
- dimensional binding  
- cycle state  

### 7.1 Attribute Structure

Each attribute entry contains:

- `id`  
- `owner` → node or relation ID  
- `type`  
- `value`  
- `dimension` (optional)  
- `metadata`  

### 7.2 Attribute Indices

Attributes are indexed by:

- ID (primary)  
- owner  
- type  

### 7.3 Attribute Memory Guarantees

- Attributes must be valid for the owner’s type and dimension  
- Closure states must be resolvable  
- No attribute may exist without an owner  

---

## 8. Metadata Memory

Metadata includes:

- runtime version  
- interpreter version  
- timestamps  
- event counters  
- status flags  
- execution metrics  

Metadata is read‑only to external systems.

---

## 9. Snapshot Model

Before each event is processed, the runtime creates a **snapshot**:

- node table  
- relation table  
- block table  
- attribute table  
- metadata  

Snapshots are:

- immutable  
- isolated  
- consistent  
- used for execution and propagation  

Snapshots prevent:

- mid‑event inconsistencies  
- partial updates  
- cascading failures  

---

## 10. Mutation Model

All mutations follow a strict sequence:

1. **Working Copy Creation**  
   A mutable copy of affected entries is created.

2. **Local Update**  
   The event’s direct changes are applied.

3. **Propagation**  
   Updates propagate through relations and blocks.

4. **Validation**  
   The working copy is validated for consistency.

5. **Commit**  
   The working copy replaces the live memory.

6. **Flag Update**  
   Runtime status flags are refreshed.

If validation fails:

- the working copy is discarded  
- the event is rejected  
- the live memory remains unchanged  

---

## 11. Memory Safety Rules

The runtime enforces:

- no dangling references  
- no orphan attributes  
- no orphan blocks  
- no invalid dimensions  
- no contradictory closure states  
- no partial updates  

Memory safety is guaranteed through:

- snapshot isolation  
- atomic commits  
- strict validation  

---

## 12. External AI Interaction

External AI systems (including Copilot) may:

- read memory via the API  
- request updates  
- enqueue events  
- inspect snapshots  

They may **not**:

- mutate memory directly  
- bypass validation  
- introduce hidden state  
- modify memory layout  

All AI interactions must pass through:

- the event loop  
- the execution model  
- the graph update engine  

---

## 13. Summary

The Memory Model defines:

- how nodes, relations, blocks, and attributes are stored  
- how memory is indexed and accessed  
- how snapshots isolate execution  
- how mutations are applied atomically  
- how consistency and safety are preserved  
- how external systems interact with memory  

This file provides the **structural substrate** that supports the entire SLP runtime.
