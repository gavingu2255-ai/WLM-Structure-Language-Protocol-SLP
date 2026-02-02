# api.md  
*Structure Language Protocol (SLP) — Runtime API Layer*

---

## 1. Purpose

The API Layer defines the **public interface** for interacting with the SLP runtime.  
It provides controlled access to:

- nodes  
- relations  
- blocks  
- attributes  
- runtime state  
- execution triggers  
- event submission  

The API is the **boundary layer** between the runtime and all external systems, including AI executors.

---

## 2. Core Principles

The API follows six principles:

1. **Safety**  
   No API call may bypass validation, execution rules, or the event loop.

2. **Determinism**  
   Identical API calls produce identical results.

3. **Isolation**  
   External systems cannot mutate internal memory directly.

4. **Atomicity**  
   Every API‑initiated update is treated as an event batch.

5. **Transparency**  
   All API calls are logged and traceable.

6. **Completeness**  
   The API exposes all necessary runtime functionality without leaking internals.

---

## 3. API Categories

The API is divided into seven categories:

1. **Node API**  
2. **Relation API**  
3. **Block API**  
4. **Attribute API**  
5. **Query API**  
6. **Execution API**  
7. **Runtime API**

Each category is described below.

---

## 4. Node API

### 4.1 `create_node(payload)`
Creates a new node.

Payload may include:

- `type`  
- `dimension`  
- `attributes`  
- `block`  

Returns:

- node ID  
- status  

### 4.2 `update_node(id, payload)`
Updates node type, dimension, or metadata.

### 4.3 `delete_node(id)`
Deletes a node and all associated relations and attributes.

---

## 5. Relation API

### 5.1 `create_relation(payload)`
Creates a relation.

Payload includes:

- `from`  
- `to`  
- `type`  
- `attributes`  

### 5.2 `update_relation(id, payload)`
Updates relation type or attributes.

### 5.3 `delete_relation(id)`
Deletes a relation.

---

## 6. Block API

### 6.1 `create_block(payload)`
Creates a block with optional parent.

### 6.2 `update_block(id, payload)`
Updates parent, metadata, or associated node.

### 6.3 `delete_block(id)`
Deletes a block after ensuring no orphan children remain.

---

## 7. Attribute API

### 7.1 `set_attribute(owner_id, type, value)`
Sets or updates an attribute on a node or relation.

### 7.2 `remove_attribute(attribute_id)`
Removes an attribute.

### 7.3 `get_attributes(owner_id)`
Returns all attributes for a node or relation.

---

## 8. Query API

### 8.1 `get_node(id)`
Returns node structure and attributes.

### 8.2 `get_relation(id)`
Returns relation structure and attributes.

### 8.3 `get_block(id)`
Returns block structure and hierarchy.

### 8.4 `find_nodes(filter)`
Filter by:

- type  
- dimension  
- block  
- attribute presence  

### 8.5 `find_relations(filter)`
Filter by:

- type  
- endpoints  
- attribute presence  

### 8.6 `get_graph_snapshot()`
Returns a read‑only snapshot of the entire graph.

---

## 9. Execution API

### 9.1 `enqueue_event(event)`
Adds an event to the event queue.

### 9.2 `tick()`
Executes one full runtime cycle:

- snapshot  
- validation  
- execution  
- propagation  
- post‑validation  
- commit  

### 9.3 `run_until_stable()`
Executes ticks until:

- no pending events  
- no dirty nodes  
- no unresolved propagation  

### 9.4 `resolve_closure(id)`
Forces closure resolution on a node.

### 9.5 `resolve_dimension(id)`
Forces dimensional resolution on a node.

---

## 10. Runtime API

### 10.1 `get_status()`
Returns:

- `WLM_STATE_SYNCHRONIZED`  
- `BUFFER_STABLE`  
- `INTEGRITY_NORMALIZED`  
- `CONSISTENCY_OK`  
- `INTENT_LOCKED`  

### 10.2 `get_metadata()`
Returns runtime metadata.

### 10.3 `reset_runtime()`
Clears runtime state (interpreter output must be reloaded).

---

## 11. API Error Model

All API errors follow a unified structure:
{ "error": "<error_code>", "message": "<human-readable description>", "details": { ... } }

Common error codes:

- `INVALID_NODE`  
- `INVALID_RELATION`  
- `INVALID_BLOCK`  
- `INVALID_ATTRIBUTE`  
- `INVALID_DIMENSION`  
- `INVALID_CLOSURE`  
- `CONFLICTING_UPDATE`  
- `VALIDATION_FAILED`  
- `UNRESOLVED_DEPENDENCY`  

Errors never leave the runtime in a partial state.

---

## 12. External AI Integration

External AI systems (including Copilot) may use the API to:

- read graph state  
- propose updates  
- enqueue events  
- trigger execution  
- perform structural reasoning  
- render human‑readable interpretations  

They may **not**:

- mutate memory directly  
- bypass validation  
- reorder events  
- override execution rules  
- introduce hidden state  

The API is the **only legal interface** for AI interaction.

---

## 13. Summary

The API Layer defines:

- how external systems interact with the runtime  
- how nodes, relations, blocks, and attributes are created and updated  
- how execution is triggered  
- how state is queried  
- how errors are handled  
- how AI systems integrate safely  

This file completes the **public boundary** of the SLP runtime.



