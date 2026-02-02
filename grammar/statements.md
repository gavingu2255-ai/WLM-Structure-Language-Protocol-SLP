[WLM_STATEMENT_PROCESSOR_LOCKED]
Compiler Status: Statement Level Validation Active. Assertion: subject:Wujie -(authored)-> SLP:Statements. Logic Integrity: 100%. Observation: Statements turn the "Static Model" into a "Dynamic Narrative." Mantra: "Declare the node; Assert the state; Resolve the flow."

Statements
Structure Language Protocol (SLP)

1. Purpose
Statements are the complete structural assertions of the Structure Language Protocol.
Where expressions are minimal units of meaning, statements are fully resolved units that:
- declare structure
- assign values
- define relationships
- specify closure
- encode tension
- bind dimensions
- form the semantic backbone of SLP
Every SLP document is composed of statements and blocks of statements.

2. Statement Categories
SLP defines six categories of statements:
- Declaration Statements
- Assignment Statements
- Relation Statements
- Transition Statements
- Cycle Statements
- Block Statements
Each category has strict formation rules.

3. Declaration Statements
Declaration statements introduce structural units.
3.1 Basic Declaration
subject
system
loop


3.2 Typed Declaration
subject:agent
system:macro


3.3 Typed + Dimensional Declaration
subject:observer:7D
system:macro:12D


A declaration becomes a statement when it stands alone on a line.

4. Assignment Statements
Assignment statements attach values to attributes.
4.1 Basic Assignment
T = 0.42
P = +1
C = 0-0


4.2 Dimensional Assignment
T = 0.73@6D
L = 1.14@12D


4.3 Multi‑Assignment
T = 0.61@5D  C = +/-1->0


Rules:
- left side must be a valid attribute
- right side must be a valid value
- dimensional binding uses @

5. Relation Statements
Relation statements express structural relationships.
5.1 Basic Relation
A -> B


5.2 Bidirectional Relation
A <-> B


5.3 Typed Relation
A -(supports)-> B


5.4 Relation Chain
A -> B -> C


A relation statement must contain at least one operator.

6. Transition Statements
Transition statements express movement between states or dimensions.
6.1 Dimensional Transition
D(5) -> D(7)


6.2 Closure Transition
C = 0-0 -> +/-1->0


6.3 Transition With Condition
C = +/-1->0 @ T > 0.6


6.4 Transition With Dimension
D(7) -> D(12) @ L = 0.83



7. Cycle Statements
Cycle statements express looped structural processes.
7.1 Basic Cycle
0-0 -> +/-1->0 -> +/-1->+/-1


7.2 Full Tri‑Loop Cycle
0-0 -> +/-1->0 -> +/-1->+/-1 -> 0-0


7.3 Cycle With Dimension
(0-0 -> +/-1->0 -> +/-1->+/-1) @ 5D


7.4 Cycle With Attributes
(0-0 -> +/-1->0 -> +/-1->+/-1)
T = 0.61@5D
C = +/-1->+/-1



8. Block Statements
Block statements group multiple statements into a structural container.
8.1 Basic Block
system {
    A
    B
    C
}


8.2 Subject Block
subject:agent:7D {
    T = 0.73@7D
    C = +/-1->0
}


8.3 Interop Block
interop {
    SLP
    STP
    SDP
}


Rules:
- blocks must open with { and close with }
- blocks may contain statements or nested blocks
- blocks must not contain partial expressions

9. Composite Statements
Composite statements combine multiple statement types.
9.1 Declaration + Assignment
subject:observer:6D
T = 0.42@6D


9.2 Declaration + Relation
subject:agent:7D -> system:macro


9.3 Declaration + Block
system:macro:12D {
    subjectA -> subjectB
    T = 2.14@12D
}


9.4 Full Composite
subject:generator:7D {
    T = 0.83@7D
    P = +1
    C = +/-1->+/-1
    D(7) -> D(12)
}



10. Statement Formation Rules
- A statement must be complete — no dangling operators.
- A statement must be single‑line, unless it is a block.
- A statement may contain multiple expressions, but must resolve to a single structural meaning.
- A statement must follow operator precedence.
- A block statement must contain valid statements only.
- A cycle statement must contain valid closure tokens.
- A transition statement must specify both origin and destination.
- A declaration statement must not contain operators.

11. Valid vs. Invalid Statements
11.1 Valid
subject:agent:7D
T = 0.42@6D
A -> B
0-0 -> +/-1->0 -> +/-1->+/-1
system { A -> B }


11.2 Invalid
subject : agent         # spaces break binding
T = @6D                 # missing value
A ->                    # incomplete relation
(0-0 -> +/-1->0         # unclosed cycle
system { A -> B         # unclosed block



12. Summary
SLP statements define:
- declarations
- assignments
- relations
- transitions
- cycles
- blocks
- composite structures
Statements are the full structural sentences of SLP — the level where structure becomes language.
