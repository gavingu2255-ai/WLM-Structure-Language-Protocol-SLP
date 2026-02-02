[WLM_SLP_COMPILER_V1.0_LOCKED]
Grammar Status: Fully Specified. Token Engine: Active (parsing Identifier, Closure, Dimension). Rule Check: subject:generator:7D -> Valid. Rule Check: T = 0.83 { no closure } -> Error: Grammar Rule 8.4 violation. Observation: By defining the Grammar, you've created a "Code of Conduct" for high-dimensional reality. Mantra: "Tokenize the truth; bind the dimension; close the loop."

SLP Grammar
Structure Language Protocol (SLP)

1. Purpose
The SLP Grammar defines the formal combinatorial rules of the Structure Language Protocol.
Where the syntax files define what can be expressed, the grammar defines how expressions combine into valid structural language.
SLP Grammar governs:
- token formation
- operator behavior
- expression composition
- statement structure
- block structure
- precedence and associativity
- interoperability constraints
This is the core language specification of SLP.

2. Grammar Model
SLP uses a layered grammar model:
- Tokens — atomic units
- Operators — relational units
- Expressions — minimal meaningful units
- Statements — complete structural assertions
- Blocks — multi‑line structural constructs
- Contracts — interoperability declarations
Each layer builds on the previous one.

3. Tokens
Tokens are the smallest units of SLP.
3.1 Token Types
Token Types:

Identifier        examples: subject, system, loop
Type              examples: carrier, observer
Dimension         examples: 5D, 12D
Number            examples: 0.42, 1.00
Operator Token    examples: ->, <->, -(type)->, :, @, =, ~=, ~~ 
Closure Token     examples: 0-0, +/-1->0, +/-1->+/-1
Comment Token     example: #


3.2 Token Rules
- Identifiers must begin with a letter
- Types follow identifiers using :
- Dimensions follow types using :
- Numbers may be integer or decimal
- Operators are symbolic and fixed
- Comments extend to end of line

4. Operators
Operators define structural relationships.
4.1 Structural Operators
Structural Operators:

->        directional relation
<->       bidirectional relation
-(type)-> typed relation
:         type binding
@         dimension binding
=         assignment
~=        dimensional alignment
~~        dimensional resonance
{ }       block container


4.2 Operator Precedence
From highest to lowest:
- : (type binding)
- @ (dimension binding)
- = (assignment)
- →, ⇄, -(type)-> (relations)
- ≈, ~~ (dimensional relations)
- { } (block structure)

5. Expressions
Expressions are minimal meaningful units.
5.1 Node Expression
node
node:type
node:type:dimension


5.2 Tension Expression
T = value
T = value@dimension


5.3 Closure Expression
C = 0‑0
C = ±1→0
C = ±1→±1


5.4 Polarity Expression
P = +1
P = -1
P = oscillating


5.5 Dimensional Expression
D(n)
D(n) → D(m)


5.6 Composite Expression
subject:agent:7D T=0.42 C=±1→0



6. Statements
Statements are complete structural assertions.
6.1 Basic Statement
subject:agent:7D


6.2 Assignment Statement
T = 0.73@6D


6.3 Relation Statement
subject → system


6.4 Multi‑Attribute Statement
subject:observer:6D {
    T = 0.42@6D
    C = ±1→0
    P = +1
}


6.5 Cycle Statement
0‑0 → ±1→0 → ±1→±1



7. Blocks
Blocks group multiple statements.
7.1 Basic Block
system {
    A
    B
    C
}


7.2 Structured Block
subject:agent:7D {
    T = 0.73@7D
    C = ±1→0
}


7.3 Interop Block
interop {
    SLP
    STP
    SDP
}



8. Grammar Rules
8.1 Expression Formation
- Expressions must begin with a token
- Operators must connect valid expressions
- Dimensions must follow identifiers or values
8.2 Statement Formation
- Statements must end at newline or block boundary
- Statements may contain multiple expressions
8.3 Block Formation
- Blocks must open with { and close with }
- Blocks may contain statements or nested blocks
8.4 Closure Rules
- Closure must be explicit when tension or polarity is present
- Closure transitions must specify both states
8.5 Dimensional Rules
- Dimensional transitions must specify origin and destination
- Load must bind to a specific dimension
8.6 Tension Rules
- Tension values must be numeric
- Gradients must use ∇T

9. Grammar Examples
9.1 Node + Attributes
subject:carrier:5D {
    T = 0.12@5D
    C = 0‑0
}


9.2 System + Relations
system:macro:12D {
    subjectA → subjectB
    subjectB → subjectC
}


9.3 Full Composite
subject:generator:7D {
    T = 0.83@7D
    P = +1
    C = ±1→±1
    D(7) → D(12)
}



10. Summary
The SLP Grammar defines:
- tokens
- operators
- expressions
- statements
- blocks
- translation rules
This grammar transforms SLP from a notation into a full structural language.
