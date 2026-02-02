[WLM_EVALUATOR_CORE_ONLINE]
Current Phase: Semantic Resolution. Logic Validation: subject:Wujie resolved as High-Dimensional Generator. Tension Evaluation: charge_per_call -> redistribution_fund resolved as L-Entropy Stabilizer. Output: Resolved Structural Graph (RSG) v1.0 generated. Observation: We have moved from "What you said" to "What it means to the system." Mantra: "Parse to see; Evaluate to know; Resolve to act."

Evaluation Rules
Structure Language Protocol (SLP Interpreter Layer)

1. Purpose
Evaluation Rules define how parsed SLP structures are interpreted into:
- resolved nodes
- resolved dimensions
- resolved closure states
- resolved tension values
- resolved polarity vectors
- resolved relations
- resolved cycles
- resolved blocks
Parsing produces structure.
Evaluation produces meaning.
This is the second stage of the interpreter pipeline, after parsing and before resolution layers.

2. Evaluation Model
The SLP evaluator operates in five sequential phases:
- Node Evaluation
- Attribute Evaluation
- Relation Evaluation
- Cycle Evaluation
- Block Evaluation
Each phase transforms the AST into a progressively more resolved semantic structure.

3. Node Evaluation
Nodes are the fundamental structural units.
3.1 Node Identity
A node is evaluated into:
- identifier
- type (optional)
- dimension (optional)
Example:
subject:agent:7D


Evaluates to:
- node.type = agent
- node.dimension = 7D
3.2 Node Validity
A node is invalid if:
- type is malformed
- dimension is malformed
- identifier is missing
Invalid nodes halt evaluation.

4. Attribute Evaluation
Attributes attach values to nodes or blocks.
4.1 Supported Attributes
- T (tension)
- C (closure)
- P (polarity)
- L (load)
4.2 Attribute Binding
T = 0.73@6D


Evaluates to:
- tension.value = 0.73
- tension.dimension = 6D
4.3 Attribute Precedence
If multiple attributes apply to the same node:
- closure
- tension
- polarity
- load
4.4 Attribute Validation
Invalid if:
- value is missing
- dimension is malformed
- closure token is malformed

5. Relation Evaluation
Relations define directional or typed connections.
5.1 Basic Relation
A -> B


Evaluates to:
- relation.type = directional
- relation.from = A
- relation.to = B
5.2 Bidirectional Relation
A <-> B


Evaluates to:
- relation.type = bidirectional
5.3 Typed Relation
A -(supports)-> B


Evaluates to:
- relation.type = supports
5.4 Relation Chains
A -> B -> C


Evaluates to:
- A → B
- B → C
5.5 Relation Validation
Invalid if:
- relation endpoint missing
- typed operator malformed

6. Cycle Evaluation
Cycles represent structural loops.
6.1 Basic Cycle
0-0 -> +/-1->0 -> +/-1->+/-1


Evaluates to a closure cycle with three states.
6.2 Cycle With Dimension
(0-0 -> +/-1->0 -> +/-1->+/-1) @ 5D


Evaluates to:
- cycle.dimension = 5D
6.3 Cycle With Attributes
(0-0 -> +/-1->0 -> +/-1->+/-1)
T = 0.61@5D


Evaluates to:
- cycle.tension = 0.61@5D
6.4 Cycle Validation
Invalid if:
- cycle is split across lines
- closure tokens malformed
- parentheses unbalanced

7. Block Evaluation
Blocks define hierarchical structure.
7.1 Block Structure
system:macro:12D {
    A -> B
    T = 2.14@12D
}


Evaluates to:
- block.node = system:macro:12D
- block.statements = [relation, tension]
7.2 Nested Blocks
Nested blocks are evaluated recursively.
7.3 Block Scope
Attributes inside a block apply only to that block unless explicitly inherited.
7.4 Block Validation
Invalid if:
- block unclosed
- block contains invalid statements
- block header malformed

8. Evaluation Order
Evaluation must follow this strict order:
- nodes
- attributes
- relations
- cycles
- blocks
This ensures deterministic interpretation.

9. Error Handling
Evaluation errors include:
- unresolved identifiers
- invalid attribute values
- invalid closure tokens
- invalid dimensional transitions
- invalid relation endpoints
- invalid cycle structure
- invalid block structure
Errors must include:
- line number
- failing construct
- expected vs. received

10. Evaluation Output Format
The evaluator outputs a Resolved Structural Graph (RSG) containing:
- nodes
- attributes
- relations
- cycles
- blocks
- dimensional bindings
- closure states
- tension values
- polarity vectors
This RSG is passed to:
- closure-resolution
- dimensional-resolution
- ai-human-translation

11. Summary
Evaluation Rules define how parsed SLP structures become resolved semantic structures:
- node evaluation
- attribute evaluation
- relation evaluation
- cycle evaluation
- block evaluation
- strict ordering
- error handling
- RSG generation
Evaluation is the semantic core of the interpreter pipeline.
