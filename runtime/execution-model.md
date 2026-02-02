execution-model.md
Structure Language Protocol (SLP) — Runtime Execution Model

1. Purpose
The Execution Model defines how the SLP runtime applies dynamic structural updates during execution.
While the interpreter produces a static Resolved Structural Graph (RSG), the execution model:
- applies closure transitions
- resolves dimensional changes
- updates tension, polarity, and load
- propagates effects across nodes and relations
- enforces block inheritance
- ensures deterministic, time‑ordered updates
The execution model is the movement layer of SLP.

2. Core Principles
The execution engine follows six principles:
- Deterministic Order
All updates follow a strict evaluation sequence.
- Atomic Transitions
Each update is applied fully or not at all.
- No Hidden State
All state changes must originate from events.
- Propagation Safety
Updates propagate only through valid relations and blocks.
- Consistency Preservation
Closure, dimension, tension, and polarity must remain valid.
- Time‑Step Isolation
Updates within a single tick cannot observe each other’s intermediate states.

3. Execution Cycle Overview
Each execution cycle (tick) consists of:
- Event Intake
- Pre‑Resolution Snapshot
- Closure Resolution
- Dimensional Resolution
- Attribute Resolution
- Propagation Phase
- Post‑Resolution Validation
- Commit Phase
This ensures deterministic, reproducible behavior.

4. Update Order
The execution engine applies updates in the following strict order:
- Closure
- Dimension
- Tension
- Polarity
- Load
- Block Inheritance
- Relation Propagation
This order prevents contradictory states and ensures stable resolution.

5. Closure Execution
Closure updates include:
- state changes
- transitions
- cycles
- conditional closure
5.1 Closure Transition Rule
If a closure transition exists:
C = A -> B


The runtime resolves to B, unless:
- a condition blocks it
- a cycle overrides it
- a block‑level closure overrides it
5.2 Closure Cycle Rule
Cycles resolve according to:
- tension
- polarity
- dimension
- block context
The active state is selected using the rules in closure-resolution.md.

6. Dimensional Execution
Dimensional updates include:
- dimensional transitions
- alignment
- resonance
- dimensional load
6.1 Dimensional Transition Rule
D(x) -> D(y)


Resolves to D(y) unless:
- a condition blocks it
- closure forces collapse
- block‑level dimension overrides it
6.2 Alignment Rule
aD ~= bD


Resolves to the closest shared dimension.
6.3 Resonance Rule
aD ~~ bD


Resolves to the higher dimension, unless tension is low.

7. Attribute Execution
Attributes update according to:
- numeric changes
- dimensional bindings
- block inheritance
- relation propagation
7.1 Tension Update Rule
Tension may:
- amplify closure
- collapse dimension
- trigger conditional transitions
7.2 Polarity Update Rule
Polarity may:
- stabilize or destabilize closure
- amplify or collapse dimension
7.3 Load Update Rule
Load influences:
- dimensional resonance
- closure intensity

8. Block Inheritance Execution
Blocks apply attributes to child nodes unless overridden.
8.1 Inheritance Order
- inner block
- outer block
- global context
8.2 Overriding Rule
Node‑level attributes always override block‑level attributes.

9. Relation Propagation Execution
Relations propagate closure, dimension, and attributes according to relation type.
9.1 Directional Propagation
A -> B


B inherits updates from A if:
- B has no conflicting attributes
- propagation is allowed
9.2 Bidirectional Propagation
A <-> B


A and B equalize attributes.
9.3 Typed Propagation
A -(supports)-> B
A -(corrects)-> B
A -(feeds)-> B


Each type has deterministic propagation rules defined in the spec.

10. Event‑Driven Execution
All updates originate from events:
- attribute changes
- node updates
- relation updates
- block updates
- external API calls
The execution engine processes events in FIFO order.

11. Time‑Step Isolation
During a single tick:
- all updates are computed using the pre‑resolution snapshot
- no update can observe another update’s intermediate state
- all updates commit simultaneously
This prevents cascading inconsistencies.

12. Post‑Resolution Validation
After updates are applied, the runtime validates:
- closure consistency
- dimensional consistency
- attribute validity
- block hierarchy
- relation integrity
Invalid states trigger errors and rollback.

13. AI Execution Interface
External AI systems (including Copilot) may:
- request execution
- apply updates
- trigger events
- read resolved states
They may not:
- bypass validation
- modify execution order
- introduce hidden state
- override runtime rules
The AI interface is defined in runtime-core.md and external-interface.md.

14. Summary
The Execution Model defines:
- the order and rules of dynamic updates
- how closure, dimension, tension, polarity, and load evolve
- how blocks and relations propagate changes
- how events drive execution
- how the runtime maintains consistency
This file gives the SLP runtime its movement, turning static structure into a living, evolving system.
