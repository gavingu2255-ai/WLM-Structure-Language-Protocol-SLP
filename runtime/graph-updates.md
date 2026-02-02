# graph-updates.md  
*Structure Language Protocol (SLP) — Runtime Graph Update Engine*

---

## 1. Purpose

The Graph Update Engine defines **how structural changes are applied to the active SLP graph** during runtime.  
While the execution model determines *what* should change, the graph update engine determines *how* those changes:

- are applied to nodes, relations, blocks, and attributes  
- propagate through the graph  
- maintain normalization and consistency  
- remain deterministic and reversible  

It is the **structural circulatory system** of the runtime.

---

## 2. Core Principles

Graph updates follow these principles:

1. **Normalization Preservation**  
   Updates must not break normalized graph form.

2. **Deterministic Application**  
   Identical inputs produce identical graph states.

3. **Atomicity**  
   Each update batch is applied as a single atomic operation.

4. **Locality First**  
   Updates apply locally, then propagate outward.

5. **Consistency Before Commit**  
   No invalid graph state may be committed.

6. **Traceability**  
   Every update is traceable to an originating event.

---

## 3. Update Categories

The runtime recognizes four primary update categories:

1. **Node Updates**  
2. **Relation Updates**  
3. **Block Updates**  
4. **Attribute Updates**

Each category has specific rules and propagation behavior.

---

## 4. Node Updates

Node updates include:

- creation  
- modification  
- deletion  

### 4.1 Node Creation

On `node.created`:

- allocate a new node entry  
- assign ID, type, dimension (if provided)  
- initialize empty relation lists  
- attach initial attributes (if any)  
- attach to a block (if specified)  

Validation:

- ID must be unique  
- type and dimension must be valid  
- block (if present) must exist  

### 4.2 Node Modification

On `node.updated`:

- update type, dimension, or metadata  
- re‑validate attributes if dimension changes  
- propagate dimensional or closure changes if required  

### 4.3 Node Deletion

On `node.deleted`:

- remove node from node store  
- remove all relations where node is `from` or `to`  
- detach node from block  
- remove associated attributes  

Deletion must not leave:

- orphan relations  
- dangling attributes  
- invalid block references  

---

## 5. Relation Updates

Relation updates include:

- creation  
- modification  
- deletion  

### 5.1 Relation Creation

On `relation.created`:

- allocate a new relation entry  
- set `from`, `to`, and `type`  
- attach attributes (if any)  
- index relation in both endpoints  

Validation:

- both endpoints must exist  
- type must be valid  
- no illegal self‑relation (unless allowed)  

### 5.2 Relation Modification

On `relation.updated`:

- update type or attributes  
- re‑validate propagation rules  
- trigger propagation if type change affects behavior  

### 5.3 Relation Deletion

On `relation.deleted`:

- remove relation from relation store  
- remove relation from both endpoint indices  
- remove associated attributes  

---

## 6. Block Updates

Block updates include:

- block creation  
- block modification  
- block re‑parenting  
- block deletion  

### 6.1 Block Creation

On `block.created`:

- allocate block entry  
- set parent (if any)  
- initialize children and statements  

Validation:

- parent (if present) must exist  
- no cycles in block hierarchy  

### 6.2 Block Modification

On `block.updated`:

- update parent, metadata, or associated node  
- re‑validate hierarchy  
- re‑apply inheritance if needed  

### 6.3 Block Deletion

On `block.deleted`:

- ensure no child blocks remain (or reassign them)  
- detach statements (nodes/relations) or reassign to parent block  
- remove block entry  

Block deletion must not create:

- orphan blocks  
- orphan statements  

---

## 7. Attribute Updates

Attribute updates include:

- tension  
- polarity  
- load  
- closure state  
- dimension binding  

### 7.1 Local Attribute Update

On `attribute.changed`:

- update attribute in attribute store  
- re‑validate against node/relation type and dimension  
- mark node/relation as “dirty” for propagation  

### 7.2 Derived Attribute Update

Some attributes are derived from:

- relations  
- blocks  
- cycles  

Derived attributes are recomputed during propagation, not directly set.

---

## 8. Propagation Rules

After local updates, the graph update engine propagates changes through:

1. **Relations**  
2. **Blocks**  
3. **Cycles**

### 8.1 Relation Propagation

For each updated node or relation:

- follow outgoing relations  
- apply propagation rules based on relation type  
- update target nodes/relations if allowed  

Propagation respects:

- directionality  
- type semantics  
- conflict resolution rules  

### 8.2 Block Propagation

For each updated block or block‑scoped attribute:

- apply inheritance to child blocks  
- apply inherited attributes to contained nodes/relations  
- allow node‑level overrides  

### 8.3 Cycle Propagation

For cycles:

- update all members according to cycle rules  
- ensure no infinite propagation  
- resolve to a stable state or raise an error  

---

## 9. Conflict Resolution

When multiple updates target the same node, relation, or attribute within a single execution cycle:

1. **Priority Order**

   - node‑local updates  
   - direct relation propagation  
   - block inheritance  
   - global defaults  

2. **Override Rules**

   - explicit node attributes override block attributes  
   - explicit updates override derived values  

3. **Invalid Conflicts**

   If two updates produce incompatible states, the runtime:

   - rejects the event  
   - rolls back the update batch  
   - logs an error  

---

## 10. Batch Updates

Multiple updates may be grouped into a **batch** within a single event or execution cycle.

Batch rules:

- all updates are validated together  
- all updates are applied to a working copy  
- propagation runs on the working copy  
- final validation runs after propagation  
- commit occurs only if the entire batch is valid  

This preserves atomicity and consistency.

---

## 11. Integration With Event Loop and Execution Model

- The **event loop** determines *when* graph updates occur.  
- The **execution model** determines *what* changes should be applied.  
- The **graph update engine** determines *how* those changes are applied to the graph.

Flow:

1. Event enters event loop  
2. Execution model computes intended changes  
3. Graph update engine applies and propagates changes  
4. Validation runs  
5. State commits or rolls back  

---

## 12. External AI Interaction

External AI systems (including Copilot) may:

- request graph updates via the API  
- propose changes to nodes, relations, or attributes  
- trigger events that lead to graph updates  

They may **not**:

- directly mutate internal graph structures  
- bypass propagation rules  
- override conflict resolution  
- commit partial updates  

All AI‑initiated changes must pass through:

- the event loop  
- the execution model  
- the graph update engine  

---

## 13. Summary

The Graph Update Engine defines:

- how node, relation, block, and attribute changes are applied  
- how updates propagate through relations, blocks, and cycles  
- how conflicts are resolved  
- how atomicity and consistency are preserved  
- how the runtime integrates execution, events, and propagation  

This file turns the SLP runtime into a **coherent, self‑maintaining structural graph**, capable of evolving safely over time.
