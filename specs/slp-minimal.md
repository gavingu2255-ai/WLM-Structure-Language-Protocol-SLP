[WLM_MINIMAL_CORE_STABILIZED]
Tier: Minimal Compliance (Level 1). Feature Set: Static Structural Primitives Only. Integrity Check: subject:Wujie -(authored)-> spec:Minimal. Logic Resolution: Deterministic & Lightweight. Observation: You have successfully created a "Safe Mode" for WLM. Even if the high-dimensional layers collapse, the basic structure of your intent remains indestructible. Mantra: "Minimum syntax; Maximum stability; Essential truth."

SLP Minimal Specification
Version 1.0 — Minimal Compliance
Status: Stable

1. Purpose
This document defines the minimal feature set required for an implementation to be considered SLP‑compliant.
It includes only:
- essential syntax
- essential operators
- essential expressions
- essential interpreter behavior
Everything else — typed relations, resonance, multi‑agent structures, narrative compatibility, extended attributes — belongs to SLP Extended.
SLP Minimal is designed for:
- lightweight interpreters
- embedded systems
- constrained environments
- educational implementations
- interoperability testing

2. Minimal Concepts
SLP Minimal includes five structural primitives:
- Node
- Type
- Dimension
- Relation
- Block
Attributes (T, C, P, L) are optional in minimal mode but allowed.
Cycles, resonance, alignment, and typed relations are excluded.

3. Minimal Syntax
3.1 Identifiers
A
subject
system
node1


3.2 Types
subject:agent
system:macro


3.3 Dimensions
5D
12D


3.4 Relations
A -> B
A <-> B


Typed relations (-(type)->) are not required.
3.5 Blocks
system {
    A -> B
}


Blocks may nest.

4. Minimal Operators
SLP Minimal requires only four operator classes:
- Structural Operators
- ->
- <->
- Binding Operator
- :
- Dimensional Operator
- @ (optional, for attributes)
- Block Operators
- {
- }
Assignment (=) is optional but supported.
Alignment (~=), resonance (~~), and typed operators are excluded.

5. Minimal Expressions
A minimal expression is one of:
identifier
identifier:type
identifier:type:dimension
attribute assignment (optional)
relation


Examples:
subject:agent:7D
A -> B
T = 0.42



6. Minimal Statements
A minimal statement is:
- a single expression
- or a relation
- or a block header
Examples:
subject:observer:6D
A -> B
system {


Statements must not contain multiple unrelated expressions.

7. Minimal Blocks
Blocks define hierarchical structure.
7.1 Block Start
identifier {


7.2 Block End
}


7.3 Block Contents
Blocks may contain:
- statements
- nested blocks
Blocks may not contain:
- cycles
- resonance
- alignment
- typed relations

8. Minimal Interpreter Requirements
An SLP Minimal interpreter must implement:
8.1 Parsing
- tokenization
- expression parsing
- statement parsing
- block parsing
8.2 Evaluation
- node evaluation
- type evaluation
- dimension evaluation
- relation evaluation
- block evaluation
8.3 Output
The interpreter must produce a Resolved Structural Graph (RSG) containing:
- nodes
- relations
- block hierarchy
- dimensions (if present)
- types (if present)
Attributes may be included but are not required.

9. Minimal Error Handling
The interpreter must detect:
- malformed identifiers
- malformed types
- malformed dimensions
- invalid relations
- unclosed blocks
- invalid operator sequences
Errors must include:
- line number
- failing construct

10. Excluded From Minimal Compliance
The following features belong to SLP Extended and are not required:
- closure states
- closure transitions
- cycles
- tension
- polarity
- load
- dimensional transitions
- alignment (~=)
- resonance (~~)
- typed relations (-(type)->)
- narrative‑compatible expressions
- multi‑agent structures
- interoperability extensions
Minimal implementations may support these, but they are not required.

11. Summary
SLP Minimal defines the smallest functional subset of the Structure Language Protocol:
- nodes
- types
- dimensions
- relations
- blocks
- basic parsing
- basic evaluation
- basic structural graph output
This specification ensures interoperability, simplicity, and deterministic behavior while keeping the protocol lightweight.
