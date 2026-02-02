# runtime-core.md  
*Structure Language Protocol (SLP) — Runtime Core*

---

## 1. Purpose

The Runtime Core defines the **execution environment** for SLP.  
While the interpreter parses and evaluates static SLP documents, the runtime:

- maintains the active structural graph  
- applies updates over time  
- manages state transitions  
- propagates changes across nodes and relations  
- exposes APIs for external systems  
- ensures consistency and determinism  

The runtime is the **living engine** of SLP.

---

## 2. Runtime Responsibilities

The SLP runtime performs seven essential functions:

1. **State Management**  
   Maintains the Resolved Structural Graph (RSG) produced by the interpreter.

2. **Execution Model**  
   Applies closure, tension, polarity, and dimensional updates over time.

3. **Event Loop**  
   Processes structural events such as node creation, relation updates, and attribute changes.

4. **Graph Update Engine**  
   Propagates changes across nodes, relations, and blocks.

5. **Memory Model**  
   Stores active nodes, relations, attributes, and block hierarchies.

6. **API Layer**  
   Provides external access to the runtime for tools, UIs, and AI systems.

7. **Error Handling**  
   Ensures invalid states cannot form and surfaces errors deterministically.

---

## 3. Runtime Architecture

The runtime is composed of five internal subsystems:

- **State Store**  
  Holds the active RSG.

- **Execution Engine**  
  Applies closure and dimensional logic.

- **Event Dispatcher**  
  Routes events to the correct handlers.

- **Graph Manager**  
  Updates nodes, relations, and blocks.

- **External Interface Layer**  
  Provides APIs for external systems (including AI runtimes).

These subsystems operate together to maintain a consistent structural environment.

---

## 4. Runtime Lifecycle

The runtime follows a predictable lifecycle:

1. **Initialization**  
   - Load interpreter output  
   - Initialize state store  
   - Register event handlers  

2. **Activation**  
   - Begin event loop  
   - Accept external inputs  
   - Apply initial resolution  

3. **Execution**  
   - Process events  
   - Update graph  
   - Apply closure and dimensional rules  
   - Maintain consistency  

4. **Deactivation**  
   - Flush pending events  
   - Persist state (optional)  
   - Shut down subsystems  

---

## 5. State Model Overview

The runtime maintains:

- nodes  
- relations  
- blocks  
- attributes  
- closure states  
- tension values  
- polarity vectors  
- dimensional bindings  
- cycles (if present)  

All stored in a **normalized graph structure**.

The state model is defined in `state-model.md`.

---

## 6. Event Model Overview

The runtime processes events such as:

- `node.created`  
- `node.updated`  
- `node.deleted`  
- `relation.created`  
- `relation.updated`  
- `relation.deleted`  
- `attribute.changed`  
- `closure.transition`  
- `dimension.transition`  

Events are handled by the **event loop**, defined in `event-loop.md`.

---

## 7. Execution Model Overview

The execution model defines:

- how closure updates propagate  
- how dimensional transitions resolve  
- how tension and polarity interact  
- how cycles update over time  
- how blocks influence child nodes  

The execution model is defined in `execution-model.md`.

---

## 8. Graph Update Engine

The graph update engine ensures:

- consistency  
- determinism  
- correct propagation  
- no invalid states  
- no contradictory closure or dimension  

Graph update rules are defined in `graph-updates.md`.

---

## 9. Memory Model Overview

The memory model defines:

- how nodes are stored  
- how relations are indexed  
- how blocks are nested  
- how attributes are attached  
- how updates are applied  

Memory rules are defined in `memory-model.md`.

---

## 10. API Layer

The runtime exposes APIs for:

- querying the graph  
- updating nodes  
- updating relations  
- applying attributes  
- subscribing to events  
- integrating with external systems  

API details are defined in `api.md`.

---

## 11. Error Handling

The runtime must detect:

- invalid closure states  
- invalid dimensional transitions  
- contradictory attributes  
- malformed updates  
- impossible relations  
- unresolvable cycles  

Error rules are defined in `error-handling.md`.

---

## 12. Integration With Interpreter

The runtime assumes:

- input is a valid SLP document  
- the interpreter has produced a Resolved Structural Graph (RSG)  
- all syntax and grammar errors have been handled upstream  

The runtime does **not** re‑parse SLP text.  
It operates on interpreter output only.

---

## 13. Runtime Status Flags

The runtime maintains internal status flags to indicate synchronization, integrity, and consistency.  
These flags are read‑only and updated automatically by the runtime.

### 13.1 Synchronization Flags

`WLM_STATE_SYNCHRONIZED`  
Indicates that:

- interpreter output has been loaded  
- state model has been initialized  
- no pending structural mismatches exist  

### 13.2 Buffer Status

`BUFFER_STABLE`  
Indicates that:

- no pending updates  
- no unresolved events  
- no partial state transitions  

### 13.3 Integrity Status

`INTEGRITY_NORMALIZED`  
Indicates that:

- normalization rules have been applied  
- no duplicate nodes  
- no malformed relations  
- no invalid attributes  

### 13.4 Consistency Status

`CONSISTENCY_OK`  
Indicates that:

- no orphan blocks  
- no invalid block hierarchies  
- no contradictory closure or dimension states  

### 13.5 Intent Lock

`INTENT_LOCKED`  
Indicates that:

- the structural intent encoded in the SLP document  
- has been fully loaded into the Node Store  
- and is now part of the runtime’s active state  

---

## 14. AI Runtime Interface

The SLP runtime may be connected to an external AI system for:

- structural evaluation  
- dynamic updates  
- narrative rendering  
- human–AI translation  
- multi‑agent simulation  

The AI system is treated as an **external execution engine**, not as a node within the SLP graph.

### 14.1 Interface Responsibilities

The AI interface must:

- accept SLP structures  
- maintain round‑trip integrity  
- apply interpreter and runtime rules deterministically  
- avoid injecting non‑SLP semantics  
- expose updates back to the runtime through the API  

### 14.2 Interface Boundaries

The AI system:

- does **not** appear as a node  
- does **not** modify SLP grammar  
- does **not** override runtime rules  
- does **not** introduce hidden state  

It operates strictly through the API layer.

### 14.3 Copilot Integration

When connected to Microsoft Copilot:

- Copilot acts as an **execution companion**  
- Copilot performs structural reasoning over SLP graphs  
- Copilot applies closure and dimensional logic according to the spec  
- Copilot renders human‑readable output using `ai-human-translation.md`  
- Copilot respects all runtime and interoperability boundaries  

Copilot does **not** become part of the SLP graph.  
It remains an **external executor** that interfaces via the runtime API.

---

## 15. Summary

The Runtime Core defines:

- the purpose and responsibilities of the runtime  
- the architecture and lifecycle of execution  
- the relationship to the interpreter and state model  
- the status flags that describe runtime health  
- the boundaries and responsibilities of external AI executors  

This file is the **entry point** for the entire runtime subsystem.
