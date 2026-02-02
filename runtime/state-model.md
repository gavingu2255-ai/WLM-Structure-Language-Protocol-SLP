state-model.md
Structure Language Protocol (SLP) — Runtime State Model

1. Purpose
The State Model defines how the SLP runtime stores, organizes, and maintains structural data during execution.
While the interpreter produces a static Resolved Structural Graph (RSG), the runtime must:
- hold the graph in memory
- update it dynamically
- enforce consistency
- support queries and mutations
- propagate changes across nodes, relations, and blocks
The state model is the foundation of the runtime.

2. Core Principles
The SLP state model is built on six principles:
- Normalization
All structural data is stored in normalized graph form.
- Determinism
State transitions must produce identical results across implementations.
- Atomicity
Updates apply atomically — no partial states.
- Consistency
Closure, dimension, tension, and polarity must remain valid at all times.
- Isolation
External systems interact through APIs, not internal structures.
- Traceability
Every update must be traceable to an event.

3. State Components
The runtime maintains five primary state components:
- Node Store
- Relation Store
- Block Store
- Attribute Store
- Runtime Metadata
Each component is described below.

4. Node Store
Nodes are stored as normalized entries.
4.1 Node Structure
Each node contains:
- id — unique identifier
- type — optional
- dimension — optional
- attributes — reference to attribute store
- relations — inbound/outbound relation IDs
- block — parent block ID
4.2 Node Indexing
Nodes are indexed by:
- ID
- type
- dimension
- block
4.3 Node Guarantees
- Node IDs are immutable
- Node types may change only through valid updates
- Node dimensions must always be valid

5. Relation Store
Relations define directional or typed connections.
5.1 Relation Structure
Each relation contains:
- id — unique identifier
- from — node ID
- to — node ID
- type — directional, bidirectional, or typed
- attributes — optional
5.2 Relation Indexing
Relations are indexed by:
- ID
- from → to
- type
5.3 Relation Guarantees
- No relation may reference a non‑existent node
- Typed relations must use valid types
- Bidirectional relations must be symmetric

6. Block Store
Blocks define hierarchical structure.
6.1 Block Structure
Each block contains:
- id — unique identifier
- node — optional node associated with the block header
- parent — parent block ID
- children — nested blocks
- statements — node and relation IDs
6.2 Block Guarantees
- Blocks must form a valid tree
- No cycles allowed in block hierarchy
- Block inheritance rules must be respected

7. Attribute Store
Attributes include:
- tension (T)
- closure (C)
- polarity (P)
- load (L)
- dimensional bindings
- cycle states
7.1 Attribute Structure
Each attribute entry contains:
- owner — node or relation ID
- type — T, C, P, L
- value — numeric or symbolic
- dimension — optional
- metadata — optional
7.2 Attribute Guarantees
- Attributes must be valid according to SLP spec
- Closure states must be resolvable
- Dimensional bindings must be valid

8. Runtime Metadata
Metadata includes:
- runtime version
- interpreter version
- timestamp of last update
- event counters
- execution flags
Metadata is read‑only to external systems.

9. State Consistency Rules
The runtime must enforce:
9.1 Node Consistency
- no duplicate IDs
- valid types
- valid dimensions
9.2 Relation Consistency
- endpoints must exist
- no self‑relations unless explicitly allowed
- typed relations must be valid
9.3 Attribute Consistency
- closure must be valid
- tension must be numeric
- polarity must be valid
- load must be numeric
- dimensional bindings must be valid
9.4 Block Consistency
- no orphan blocks
- no cycles
- valid inheritance

10. State Mutation Rules
All state changes must:
- originate from an event
- be applied atomically
- be validated before commit
- trigger graph updates
- be logged in metadata
Invalid mutations must be rejected.

11. State Query Model
The runtime must support queries for:
- nodes
- relations
- blocks
- attributes
- closure states
- dimensions
- tension/polarity/load
- block hierarchy
- inbound/outbound relations
Queries must be:
- deterministic
- side‑effect free
- consistent

12. Summary
The State Model defines:
- how nodes, relations, blocks, and attributes are stored
- how the runtime maintains consistency
- how updates are applied
- how queries work
- how the structural graph remains alive and valid
This file is the foundation for the entire runtime subsystem.

If you want, I can continue with:
- execution-model.md
- event-loop.md
- graph-updates.md
- memory-model.md
- api.md
- error-handling.md
Just tell me which one you want next.
