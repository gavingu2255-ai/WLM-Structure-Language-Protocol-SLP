[WLM_SLP_COMPILER_READY]
Syntax Mode: Structural Primitives. Status: Parsing system:agent clusters. Observation: The use of # structural comments allows for narrative "tagging" without polluting the 27D logic flow. Logic Rule: Every A → B is a commitment of tension. Mantra: "Define the node, bind the loop, contain the system."

Structural Syntax
Structure Language Protocol (SLP)

1. Purpose
Structural Syntax defines how structure itself is expressed in SLP.
It provides the formal rules for representing:
- nodes
- edges
- loops
- cycles
- systems
- subjects
- structural roles
- structural relationships
This is the lowest-level syntax layer of SLP — everything else (dimensions, closure, tension, semantics) attaches to these primitives.

2. Structural Units
SLP structural expressions are built from five core units:
- Node
- Edge
- Loop
- Cycle
- System
Each unit has a standard syntax form.

3. Node Syntax
A node is the atomic structural unit.
3.1 Basic Node
[node]


3.2 Typed Node
[node:type]


Examples:
subject
subject:carrier
system:macro
loop:correction


3.3 Dimensional Node (structural only)
Dimensions are optional here; full dimensional syntax is defined separately.
[node:type:dimension]


Example:
subject:agent:5D



4. Edge Syntax
An edge expresses a structural relationship between nodes.
4.1 Basic Edge
A → B


4.2 Typed Edge
A -(relation)-> B


Examples:
subject → system
node -(supports)-> node
loop -(feeds)-> cycle


4.3 Bidirectional Edge
A ⇄ B


4.4 Edge Chains
A → B → C



5. Loop Syntax
A loop is a self-contained structural process.
5.1 Basic Loop
(loop)


5.2 Typed Loop
(loop:type)


Examples:
(loop:carrier)
(loop:correction)
(loop:generation)


5.3 Loop with Node Binding
node → (loop:type)



6. Cycle Syntax
A cycle is a sequence of loops or structural states.
6.1 Basic Cycle
[A → B → C]


6.2 Loop Cycle
(loop1) → (loop2) → (loop3)


6.3 Tri‑Loop Cycle (SLP standard)
(0‑0) → (±1→0) → (±1→±1) → (0‑0)



7. System Syntax
A system is a structural container.
7.1 Basic System
system


7.2 Typed System
system:type


Examples:
system:micro
system:macro
system:agent
system:dimensional


7.3 System with Components
system {
    A
    B
    C
}


7.4 System with Edges
system {
    A → B
    B → C
}



8. Structural Roles
Nodes may carry structural roles.
8.1 Role Syntax
node(role)


Examples:
subject(carrier)
subject(generator)
system(stabilizer)


8.2 Role Chains
node(role1, role2)



9. Composite Structures
SLP supports composite structural expressions.
9.1 Node + Loop
subject → (loop:correction)


9.2 Node + Cycle
subject → [A → B → C]


9.3 System + Cycle
system:macro {
    (0‑0) → (±1→0) → (±1→±1)
}



10. Structural Comments
SLP supports structural comments using #.
# this node stabilizes the system
subject:carrier



11. Structural Expression Rules
- Nodes are atomic — they cannot be decomposed in structural syntax.
- Edges define relationships — direction matters.
- Loops define processes — they are self-contained.
- Cycles define sequences — they must be closed or explicitly open.
- Systems define containers — they hold nodes, edges, loops, or cycles.
- Roles modify nodes — they do not replace types.
- Structure is dimension‑agnostic — dimensional syntax attaches later.

12. Summary
Structural Syntax defines the foundational building blocks of SLP:
- nodes
- edges
- loops
- cycles
- systems
- roles
These primitives form the structural layer on which dimensional, closure, tension, and semantic layers are built.
