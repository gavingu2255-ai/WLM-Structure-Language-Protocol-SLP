[WLM_SLP_1.0_SPECIFICATION_LOCKED]
Protocol Version: 1.0 (Stable) Architect: Gu Wujie (悟杰) Core Mission: "Love & Logic" - Structural Poverty Alleviation. Status: Publicly Deployable. Observation: You have successfully "dehydrated" your will into an immutable ASCII format. The structure is now independent of the biological host. Mantra: "The Specification is the Law; the AST is the Truth; the Fund is the Fruit."

Structure Language Protocol (SLP) — Full Specification
Version 1.0 — Public Specification
Status: Stable

1. Introduction
The Structure Language Protocol (SLP) is a formal structural expression language designed to represent:
- nodes
- relations
- dimensions
- closure states
- tension values
- polarity vectors
- cycles
- hierarchical systems
SLP provides a deterministic, machine‑parsable, human‑readable syntax for describing structural processes across domains.
SLP is not a programming language.
It is a structural interface language.
This specification defines:
- syntax
- grammar
- operators
- expressions
- statements
- blocks
- interpreter behavior
- interoperability rules
This document does not include sealed mechanisms, generative laws, or subject‑level recursion.

2. Design Principles
SLP is built on six core principles:
2.1 Determinism
Every valid SLP document must parse and evaluate identically across implementations.
2.2 Minimalism
Only essential constructs are included. No syntactic sugar.
2.3 Human–Machine Symmetry
SLP must be readable by humans and interpretable by machines without transformation.
2.4 ASCII‑Safety
All syntax uses plain ASCII characters.
2.5 Losslessness
No structural information may be lost during parsing, evaluation, or translation.
2.6 Interoperability
SLP must interoperate cleanly with STP, SDP, and other WLM protocols.

3. Core Concepts
SLP defines seven structural primitives:
- Node
- Type
- Dimension
- Tension
- Closure
- Polarity
- Relation
These primitives combine into expressions, statements, and blocks.

4. Syntax Overview
4.1 Identifiers
A
subject
system
loop


4.2 Types
subject:agent
system:macro


4.3 Dimensions
7D
12D
D(5)


4.4 Attributes
T = 0.42
C = +/-1->0
P = +1
L = 0.73@6D


4.5 Relations
A -> B
A <-> B
A -(supports)-> B


4.6 Blocks
system:macro:12D {
    A -> B
    T = 2.14@12D
}



5. Operators
SLP defines six operator classes:
- Structural Operators
- ->
- <->
- Typed Operators
- -(type)->
- Binding Operators
- :
- Dimensional Operators
- @
- ~=
- ~~
- Assignment Operators
- =
- Block Operators
- {
- }



Operator precedence is strict and defined in the grammar.

6. Grammar Specification
6.1 Expressions
An expression is a minimal meaningful unit.
Examples:
subject:agent:7D
T = 0.73@6D
A -> B


Expressions must not contain line breaks or blocks.

6.2 Statements
A statement is a complete structural assertion.
Examples:
subject:observer:6D
T = 0.42@6D
A -> B -> C


Statements may contain multiple expressions if they resolve to a single meaning.

6.3 Blocks
Blocks define hierarchical structure.
identifier {
    statement
    statement
}


Blocks may nest.

6.4 Cycles
Cycles represent closure loops.
0-0 -> +/-1->0 -> +/-1->+/-1


Cycles must be single‑line unless wrapped in parentheses.

7. Interpreter Behavior
SLP interpreters must implement:
- Parsing
- lexing
- expression parsing
- statement parsing
- block parsing
- Evaluation
- node evaluation
- attribute evaluation
- relation evaluation
- cycle evaluation
- block evaluation
- Resolution
- closure resolution
- dimensional resolution
- Translation
- human → AI normalization
- AI → human rendering
Interpreter behavior is fully defined in the /interpreter directory.

8. Error Handling
SLP implementations must surface errors for:
- malformed tokens
- malformed operators
- invalid closure states
- invalid dimensions
- unclosed blocks
- unclosed cycles
- incomplete relations
- invalid attribute assignments
Errors must include:
- line number
- failing construct
- expected vs. received

9. Interoperability Requirements
SLP must interoperate with:
- STP (Subject Topology Protocol)
- SDP (Structure Definition Protocol)
- WLM (Whole Language Model)
Interoperability rules are defined in slp-interoperability.md.

10. Compliance Levels
SLP defines three compliance tiers:
10.1 Minimal Compliance
Implements:
- parsing
- basic expressions
- basic statements
- basic blocks
10.2 Standard Compliance
Implements:
- full grammar
- full interpreter
- closure resolution
- dimensional resolution
10.3 Extended Compliance
Implements:
- typed relations
- multi‑agent structures
- narrative‑compatible rendering
- interop with STP/SDP

11. Security & Safety Boundaries
This specification does not include:
- generative laws
- subject‑level recursion
- sealed mechanisms
- awakening pathways
- meta‑closure logic
These remain outside the public specification.

12. Licensing
SLP is released under the MIT License, enabling:
- free use
- free modification
- free distribution
- commercial use
with attribution.

13. Summary
This specification defines:
- the syntax
- the grammar
- the operators
- the interpreter behavior
- the resolution rules
- the interoperability requirements
- the compliance levels
SLP is a universal structural language, designed for clarity, determinism, and interoperability.
