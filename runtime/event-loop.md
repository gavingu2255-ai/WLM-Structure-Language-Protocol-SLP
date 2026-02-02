event-loop.md
Structure Language Protocol (SLP) — Runtime Event Loop

1. Purpose
The Event Loop is the central dispatcher of the SLP runtime.
It controls:
- how events are received
- how they are ordered
- how they are processed
- how they trigger execution
- how updates propagate
- how the runtime maintains determinism
If the execution model is the muscle, the event loop is the nervous system.

2. Core Principles
The event loop follows six principles:
- FIFO Ordering
Events are processed strictly in the order they arrive.
- Atomic Processing
Each event is fully resolved before the next begins.
- Snapshot Isolation
Execution uses a pre‑resolution snapshot of state.
- Deterministic Resolution
Identical event sequences produce identical results.
- No Hidden Events
All events must be explicit and logged.
- Error Containment
Invalid events fail without corrupting state.

3. Event Types
The runtime recognizes the following event categories:
3.1 Node Events
- node.created
- node.updated
- node.deleted
3.2 Relation Events
- relation.created
- relation.updated
- relation.deleted
3.3 Attribute Events
- attribute.changed
- tension.changed
- polarity.changed
- load.changed
- dimension.changed
- closure.changed
3.4 Block Events
- block.entered
- block.exited
- block.updated
3.5 External Events
- API calls
- AI‑initiated updates
- system triggers
All events follow the same lifecycle.

4. Event Lifecycle
Each event passes through eight phases:
- Enqueue
Event enters the event queue.
- Dequeue
Event is removed from the queue in FIFO order.
- Snapshot
Runtime captures a read‑only snapshot of current state.
- Validation
Event is checked for structural validity.
- Execution
Event triggers the execution model.
- Propagation
Updates propagate through relations and blocks.
- Post‑Validation
Runtime ensures no invalid states were created.
- Commit
Updates are applied atomically.
If any phase fails, the event is rejected and state is rolled back.

5. Event Queue
The event queue is a strict FIFO buffer.
5.1 Queue Guarantees
- no reordering
- no parallel execution
- no starvation
- no hidden events
- no implicit batching
5.2 Queue Structure
Each entry contains:
- event type
- payload
- timestamp
- origin (interpreter, API, AI, system)
- metadata

6. Snapshot Isolation
Before processing an event, the runtime creates a snapshot:
- nodes
- relations
- blocks
- attributes
- closure states
- dimensions
The execution engine uses this snapshot to compute updates.
This ensures:
- no mid‑event inconsistencies
- no cascading partial updates
- deterministic behavior

7. Event Validation
Validation ensures:
- node IDs exist
- relation endpoints exist
- attributes are valid
- closure/dimension transitions are legal
- block hierarchy is intact
Invalid events are rejected before execution.

8. Event Execution
Once validated, the event is passed to the execution engine.
The execution engine:
- applies closure transitions
- resolves dimensional changes
- updates tension/polarity/load
- applies block inheritance
- propagates updates through relations
Execution rules are defined in execution-model.md.

9. Propagation Phase
After execution, updates propagate through:
- directional relations
- bidirectional relations
- typed relations
- block inheritance
Propagation is deterministic and follows the rules in graph-updates.md.

10. Post‑Resolution Validation
After propagation, the runtime checks:
- closure consistency
- dimensional consistency
- attribute validity
- block hierarchy
- relation integrity
If validation fails:
- event is rejected
- state is rolled back
- error is logged

11. Commit Phase
If validation succeeds:
- updates are applied atomically
- metadata is updated
- status flags are refreshed
- event is marked as resolved
This completes the event lifecycle.

12. External AI Event Integration
External AI systems (including Copilot) may:
- enqueue events
- request execution
- read snapshots
- apply updates through the API
They may not:
- bypass the event loop
- reorder events
- inject hidden events
- modify execution rules
AI systems operate strictly through the API layer.

13. Runtime Status Flag Updates
The event loop updates:
- BUFFER_STABLE
- INTEGRITY_NORMALIZED
- CONSISTENCY_OK
- WLM_STATE_SYNCHRONIZED
- INTENT_LOCKED
Flags are updated after each commit.

14. Summary
The Event Loop defines:
- how events enter and move through the runtime
- how updates are validated, executed, propagated, and committed
- how the runtime maintains determinism and consistency
- how external systems interact safely
This file gives the SLP runtime its nervous system, enabling controlled, predictable structural evolution.
