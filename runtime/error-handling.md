# error-handling.md  
*Structure Language Protocol (SLP) — Runtime Error Handling Model*

---

## 1. Purpose

The Error Handling Model defines **how the SLP runtime detects, classifies, reports, and responds to invalid structural states**.  
Its purpose is to ensure:

- no corrupted graph states  
- no partial updates  
- no silent failures  
- no hidden inconsistencies  
- deterministic, reversible behavior  

Error handling is the **immune system** of the runtime.

---

## 2. Core Principles

The runtime follows seven error‑handling principles:

1. **Fail Fast**  
   Invalid states are detected as early as possible.

2. **Fail Safe**  
   No invalid state is ever committed.

3. **Atomicity**  
   If any part of an update fails, the entire update is rolled back.

4. **Determinism**  
   Identical invalid inputs produce identical errors.

5. **Transparency**  
   All errors are explicit, structured, and logged.

6. **Isolation**  
   Errors in one event cannot affect other events.

7. **No Hidden State**  
   Errors cannot leave behind partial or inconsistent memory.

---

## 3. Error Categories

Errors fall into six categories:

1. **Node Errors**  
2. **Relation Errors**  
3. **Block Errors**  
4. **Attribute Errors**  
5. **Execution Errors**  
6. **Runtime Errors**

Each category has specific codes and conditions.

---

## 4. Node Errors

### 4.1 `INVALID_NODE`
Triggered when:

- node does not exist  
- node ID is malformed  
- node type is invalid  

### 4.2 `NODE_CONFLICT`
Triggered when:

- two updates attempt incompatible changes  
- node violates dimension or closure constraints  

### 4.3 `NODE_ORPHANED`
Triggered when:

- node is assigned to a non‑existent block  

---

## 5. Relation Errors

### 5.1 `INVALID_RELATION`
Triggered when:

- relation does not exist  
- endpoints do not exist  
- relation type is invalid  

### 5.2 `RELATION_CONFLICT`
Triggered when:

- propagation rules produce contradictory updates  

### 5.3 `RELATION_ORPHANED`
Triggered when:

- relation references a deleted node  

---

## 6. Block Errors

### 6.1 `INVALID_BLOCK`
Triggered when:

- block does not exist  
- block ID is malformed  

### 6.2 `BLOCK_CYCLE`
Triggered when:

- block hierarchy forms a cycle  

### 6.3 `BLOCK_ORPHANED`
Triggered when:

- block has no valid parent  
- deletion would leave orphan children  

---

## 7. Attribute Errors

### 7.1 `INVALID_ATTRIBUTE`
Triggered when:

- attribute type is invalid  
- attribute value is invalid  
- attribute owner does not exist  

### 7.2 `ATTRIBUTE_CONFLICT`
Triggered when:

- closure, dimension, tension, polarity, or load produce contradictions  

### 7.3 `ATTRIBUTE_OUT_OF_RANGE`
Triggered when:

- numeric attributes exceed allowed ranges  

---

## 8. Execution Errors

### 8.1 `INVALID_CLOSURE`
Triggered when:

- closure transition is illegal  
- closure cycle cannot resolve  

### 8.2 `INVALID_DIMENSION`
Triggered when:

- dimensional transition is illegal  
- dimension binding is invalid  

### 8.3 `UNRESOLVED_DEPENDENCY`
Triggered when:

- execution requires data not yet available  

### 8.4 `EXECUTION_CONFLICT`
Triggered when:

- two propagation paths produce incompatible results  

---

## 9. Runtime Errors

### 9.1 `VALIDATION_FAILED`
Triggered when:

- post‑resolution validation fails  

### 9.2 `INTERNAL_ERROR`
Triggered when:

- unexpected runtime failure  
- memory corruption detected  
- invariant violation  

### 9.3 `API_VIOLATION`
Triggered when:

- external system attempts illegal operation  
- direct memory mutation is attempted  

---

## 10. Error Lifecycle

Errors follow a strict lifecycle:

1. **Detection**  
   Error is identified during validation, execution, or propagation.

2. **Classification**  
   Error is assigned a category and code.

3. **Rollback**  
   Working copy is discarded; live memory remains unchanged.

4. **Logging**  
   Error is recorded in runtime metadata.

5. **Response**  
   API returns structured error response.

6. **Status Update**  
   Runtime flags may update (e.g., `BUFFER_STABLE = false`).

---

## 11. Error Response Format

All errors follow a unified structure:
{ "error": "<error_code>", "message": "<description>", "details": { "event": "<event_id>", "node": "<node_id>", "relation": "<relation_id>", "block": "<block_id>", "attribute": "<attribute_id>" } }

Fields not relevant to the error are omitted.

---

## 12. Rollback Model

Rollback guarantees:

- no partial updates  
- no corrupted memory  
- no inconsistent propagation  

Rollback is triggered automatically when:

- validation fails  
- propagation fails  
- execution fails  
- conflict resolution fails  
- API call violates constraints  

Rollback restores:

- node memory  
- relation memory  
- block memory  
- attribute memory  
- metadata (except error logs)  

---

## 13. Integration With Event Loop

The event loop:

- detects errors  
- halts execution  
- triggers rollback  
- logs the error  
- marks the event as failed  
- resumes with the next event  

Errors do **not** stop the runtime.

---

## 14. External AI Error Handling

External AI systems (including Copilot):

- receive structured error responses  
- may retry with corrected input  
- may not override or suppress errors  
- may not bypass rollback  
- may not force commit of invalid states  

AI systems must treat errors as **hard boundaries**, not suggestions.

---

## 15. Summary

The Error Handling Model defines:

- how errors are detected, classified, and reported  
- how rollback preserves consistency  
- how invalid states are prevented  
- how the runtime integrates error handling with execution and events  
- how external systems interact safely  

This file completes the **runtime immune system**, ensuring SLP remains stable, deterministic, and structurally sound.

