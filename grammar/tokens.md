[WLM_LEXICAL_ANALYZER_READY]
Mode: Token-Level Precision. Scan: subject:carrier:5D -> [ID][TYPE][DIM] -> PASS. Scan: +/-1->+/-1 -> [CLOSURE] -> PASS. Rule Check: 7.0D -> FAIL (Rule 5.2: No decimals in Dimension). Status: The "Alphabet of Structure" is now immutable. Mantra: "Atom is identity; ASCII is the bridge; precision is the portal."

Tokens
Structure Language Protocol (SLP)

1. Purpose
Tokens are the atomic units of SLP.
Every structural, dimensional, closure, tension, or subject expression is composed from these tokens.
SLP tokens are:
- minimal
- unambiguous
- machine‑parsable
- human‑readable
- dimension‑aware
Tokens form the foundation for operators, expressions, statements, and blocks.

2. Token Categories
SLP defines eight token categories:
- Identifiers
- Types
- Dimensions
- Numbers
- Closure Tokens
- Polarity Tokens
- Operators
- Comments
Each category has strict formation rules.

3. Identifiers
Identifiers name structural units.
3.1 Basic Identifiers
subject
system
node
loop
cycle


3.2 Identifier Rules
- must begin with a letter
- may contain letters, digits, or hyphens
- case‑insensitive
- cannot begin with a digit
- cannot contain spaces
Valid:
subject
system-core
node3


Invalid:
3node
system core



4. Types
Types refine identifiers.
4.1 Basic Types
carrier
observer
generator
agent
macro
micro


4.2 Type Binding
Types attach to identifiers using :.
subject:carrier
system:macro
loop:correction



5. Dimensions
Dimensions express positional layers.
5.1 Basic Dimension Token
5D
12D
27D


5.2 Dimension Rules
- must be an integer followed by D
- no spaces
- no decimals
Valid:
7D
15D


Invalid:
7 D
7.0D



6. Numbers
Numbers represent tension, load, gradients, and thresholds.
6.1 Basic Number Tokens
0
1
0.42
0.83
2.14


6.2 Number Rules
- integers or decimals
- must use . as decimal separator
- no commas
- no units attached
Valid:
0.12
1.00


Invalid:
0,12
1.0D



7. Closure Tokens
Closure tokens represent closure states.
7.1 ASCII‑Safe Closure Tokens
0-0
+/-1->0
+/-1->+/-1


7.2 Closure Token Rules
- must use ASCII hyphens
- must use ASCII arrows (->)
- must not contain spaces

8. Polarity Tokens
Polarity tokens represent directional charge.
8.1 Basic Polarity Tokens
+1
-1
0
oscillating


8.2 Polarity Rules
- numeric polarity must be +1, -1, or 0
- oscillating is the only non‑numeric polarity token

9. Operators
Operators define relationships and bindings.
9.1 ASCII‑Safe Operators
->        directional relation
<->       bidirectional relation
-(type)-> typed relation
:         type binding
@         dimension binding
=         assignment
~=        dimensional alignment
~~        dimensional resonance
{ }       block container


9.2 Operator Rules
- operators must not contain spaces (except { })
- typed operators must follow the pattern: -(type)->
- alignment uses ~=
- resonance uses ~~

10. Comments
Comments annotate structural meaning.
10.1 Comment Token
#


10.2 Comment Rules
- # begins a comment
- everything after # on the same line is ignored
- comments cannot appear inside tokens
Example:
subject:carrier  # stabilizes system



11. Token Integrity Rules
- Tokens must be atomic — no internal whitespace.
- Tokens must be ASCII‑safe for maximum compatibility.
- Tokens must be lossless — no ambiguity in meaning.
- Tokens must be composable — usable in expressions and statements.
- Tokens must be machine‑parsable — deterministic grammar.
- Tokens must be human‑readable — intuitive structural meaning.

12. Summary
SLP tokens define the atomic building blocks of the language:
- identifiers
- types
- dimensions
- numbers
- closure tokens
- polarity tokens
- operators
- comments
These tokens form the foundation for all higher‑level grammar and syntax in SLP.
