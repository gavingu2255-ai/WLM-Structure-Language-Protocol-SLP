# runtime-tests.md  
*Structure Language Protocol (SLP) — Runtime Execution Test Suite*

---

## 1. Purpose

Runtime tests verify that the **SLP Runtime Engine**:

- processes events in FIFO order  
- applies execution rules correctly  
- updates the graph deterministically  
- propagates changes through relations and blocks  
- maintains snapshot isolation  
- commits only valid states  
- rolls back invalid states  
- updates runtime status flags correctly  

Runtime tests run **after resolution tests** and represent the first full end‑to‑end execution layer.

---

## 2. Test Categories

Runtime tests are grouped into:

1. **Event Loop Tests**  
2. **Execution Cycle Tests**  
3. **Propagation Tests**  
4. **Block Inheritance Runtime Tests**  
5. **Cycle Execution Tests**  
6. **Atomicity & Rollback Tests**  
7. **Status Flag Tests**  
8. **Mixed Runtime Tests**  
9. **Invalid Runtime Tests**

Each category includes expected post‑execution graph state.

---

## 3. Event Loop Tests

### 3.1 FIFO Ordering

Events:
- set_attribute(NodeA, tension=0.5)
- set_attribute(NodeA, tension=0.9)

Expected:
- Final tension = 0.9  
- No reordering  

### 3.2 Snapshot Isolation

Events:


- set_attribute(NodeA, tension=0.5)
- set_attribute(NodeA, tension=NodeA.tension + 0.5)

Expected:
- Second event sees tension = 0.5  
- Final tension = 1.0  

---

## 4. Execution Cycle Tests

### 4.1 Single Tick Execution

Input:


NodeA { tension: 0.5 }

Event:


tick()

Expected:
- No changes (no pending events)  
- Runtime stable  

### 4.2 Multi‑Tick Execution

Events:


set_attribute(NodeA, tension=0.5) set_attribute(NodeA, tension=0.8) run_until_stable()

Expected:
- Final tension = 0.8  
- No dirty nodes  

---

## 5. Propagation Tests

### 5.1 Directional Propagation

Graph:


A { tension: 0.5 } A -> B

Event:


tick()

Expected:
- B tension = 0.5  

### 5.2 Bidirectional Propagation

Graph:


A { tension: 0.3 } B { tension: 0.9 } A <-> B

Event:


tick()

Expected:
- A tension = 0.9  
- B tension = 0.9  

### 5.3 Typed Propagation

Graph:


A { polarity: +1 } A -(supports)-> B

Event:


tick()

Expected:
- B polarity = +1  

---

## 6. Block Inheritance Runtime Tests

### 6.1 Block Attribute Application

Graph:


BlockA { tension: 0.4 NodeA }

Event:


tick()

Expected:
- NodeA tension = 0.4  

### 6.2 Nested Block Inheritance

Graph:


BlockA { tension: 0.2 BlockB { polarity: +1 NodeA } }

Event:


tick()

Expected:
- NodeA tension = 0.2  
- NodeA polarity = +1  

---

## 7. Cycle Execution Tests

### 7.1 Two‑Node Cycle

Graph:


A -> B B -> A A { tension: 0.7 }

Event:


tick()

Expected:
- B tension = 0.7  
- A tension = 0.7  

### 7.2 Multi‑Node Cycle

Graph:


A -> B B -> C C -> A A { dimension: 4 }

Event:


tick()

Expected:
- B dimension = 4  
- C dimension = 4  

---

## 8. Atomicity & Rollback Tests

### 8.1 Partial Update Rejection

Events:


set_attribute(NodeA, tension=0.5) set_attribute(NodeA, tension="invalid")

Event:


run_until_stable()

Expected:
- First event applied  
- Second event rejected  
- NodeA tension = 0.5  

### 8.2 Propagation Conflict Rollback

Graph:


A { tension: 0.5 } B { tension: 0.9 } A <-> B

Event:


set_attribute(A, tension="invalid")

Expected:
- Entire event rejected  
- No changes to A or B  

---

## 9. Status Flag Tests

### 9.1 Synchronization Flag

After interpreter load:
- `WLM_STATE_SYNCHRONIZED = true`

### 9.2 Buffer Stability

After all events processed:
- `BUFFER_STABLE = true`

### 9.3 Integrity Normalization

After tick:
- `INTEGRITY_NORMALIZED = true`

### 9.4 Consistency Flag

After propagation:
- `CONSISTENCY_OK = true`

### 9.5 Intent Lock

After initial load:
- `INTENT_LOCKED = true`

---

## 10. Mixed Runtime Tests

### 10.1 Full Mixed Example

Graph:


BlockA { tension: 0.3 NodeA(type:entity) NodeB(dimension:2) NodeA -> NodeB NodeB { polarity: +1 } }

Event:


run_until_stable()

Expected:
- NodeA tension = 0.3  
- NodeB tension = 0.3  
- NodeB polarity = +1  
- NodeB dimension = 2  

### 10.2 Multi‑Block Mixed Example

Graph:


BlockA { tension: 0.2 NodeA BlockB { polarity: +1 NodeB NodeA -> NodeB } }

Event:


run_until_stable()

Expected:
- NodeA tension = 0.2  
- NodeB tension = 0.2  
- NodeB polarity = +1  

---

## 11. Invalid Runtime Tests

### 11.1 Impossible Closure

Graph:


NodeA { closure: A -> A }

Event:


tick()

Expected:
- runtime error  
- no commit  

### 11.2 Dimension Conflict

Graph:


A(dimension:2) B(dimension:5) A <-> B

Event:


tick()

Expected:
- runtime error  
- no commit  

### 11.3 Block Cycle

Graph:


BlockA { BlockB { BlockA } }

Event:


tick()

Expected:
- runtime error  
- no commit  

---

## 12. Summary

This test suite verifies that the Runtime Engine:

- processes events deterministically  
- applies execution rules correctly  
- propagates updates through relations and blocks  
- resolves cycles  
- maintains atomicity and rollback  
- updates status flags  
- rejects invalid runtime states  

Runtime tests ensure that the SLP runtime behaves as a **stable, deterministic execution environment** for structural evolution.

