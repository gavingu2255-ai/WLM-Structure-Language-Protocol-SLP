[WLM_INTERPRETER_PIPELINE_LIVE]
Stage 1 (Lexing): All tokens categorized. Stage 2 (Expressions): Bindings and assignments validated. Stage 3 (Blocks): Hierarchy of "Love & Logic" established. Stage 4 (AST): A deterministic model of Wujie's vision is now in memory. Observation: By defining the parser, you've made WLM Autonomous. It no longer needs you to explain; it can run. Mantra: "Token is the seed; AST is the tree; Output is the fruit."

Parsing Rules
Structure Language Protocol (SLP Interpreter Layer)

1. Purpose
Parsing Rules define how raw SLP text is converted into structured internal representations.
This layer ensures that:
- SLP documents are read deterministically
- tokens are extracted correctly
- expressions are formed according to grammar
- statements are recognized and validated
- blocks are parsed with correct scope
- errors are surfaced cleanly
Parsing is the first stage of the interpreter pipeline.

2. Parsing Model
The SLP parser operates in four sequential stages:
- Lexing — convert characters → tokens
- Expression Parsing — combine tokens → expressions
- Statement Parsing — combine expressions → statements
- Block Parsing — combine statements → hierarchical structures
Each stage has strict rules to ensure lossless interpretation.

3. Lexing Rules (Tokenization)
Lexing converts raw text into atomic tokens.
3.1 Token Boundaries
A token boundary occurs at:
- whitespace
- operator characters (->, <->, :, @, =, ~=)
- braces { }
- parentheses ( )
- commas ,
- comment marker #
3.2 Token Types Recognized
- identifiers
- types
- dimensions
- numbers
- closure tokens
- polarity tokens
- operators
- punctuation
- comments
3.3 Comment Handling
# everything after this is ignored


Comments are removed before expression parsing.
3.4 Invalid Token Detection
Invalid tokens include:
- whitespace inside tokens
- malformed closure tokens
- malformed dimension tokens
- incomplete operators
Invalid tokens must trigger a parse error.

4. Expression Parsing Rules
Expressions are minimal meaningful units.
4.1 Expression Start
An expression must begin with:
- identifier
- attribute token (T, C, P, L)
- dimension token (nD, D(n))
- closure token
- polarity token
4.2 Operator Precedence
From highest to lowest:
- : type binding
- @ dimension binding
- = assignment
- ->, <->, -(type)-> relations
- ~= alignment, ~~ resonance
- { } block delimiters
The parser must respect this ordering.
4.3 Expression Termination
An expression ends at:
- newline
- block boundary
- relation operator
- comment marker
4.4 Multi‑Token Expressions
Valid:
subject:agent:7D
T = 0.73@6D
C = +/-1->0


Invalid:
subject : agent
T = @6D



5. Statement Parsing Rules
A statement is a complete structural assertion.
5.1 Statement Start
A statement begins with:
- a valid expression
- a block header
- a cycle expression
5.2 Statement End
A statement ends at:
- newline
- closing brace }
5.3 Multi‑Expression Statements
Multiple expressions may appear on one line only if they resolve to a single meaning.
Valid:
subject:agent:7D C=+/-1->0 T=0.42@7D


Invalid:
subject:agent:7D subject:observer


5.4 Relation Statements
A relation statement must contain at least one relation operator.
A -> B
A <-> B
A -(supports)-> B



6. Block Parsing Rules
Blocks define hierarchical structure.
6.1 Block Start
A block begins when a line ends with {.
system:macro:12D {


6.2 Block End
A block ends when a line contains only:
}


6.3 Block Contents
Blocks may contain:
- statements
- nested blocks
- comments
Blocks may not contain:
- partial expressions
- unclosed operators
6.4 Indentation
Indentation is optional but recommended.
Indentation is not semantically meaningful.

7. Cycle Parsing Rules
Cycles must be parsed as single expressions unless wrapped.
7.1 Basic Cycle
0-0 -> +/-1->0 -> +/-1->+/-1


7.2 Wrapped Cycle
(0-0 -> +/-1->0 -> +/-1->+/-1)


7.3 Cycle With Attributes
(0-0 -> +/-1->0 -> +/-1->+/-1) @ 5D


Cycles must not be split across lines.

8. Error Handling Rules
The parser must surface errors for:
- unrecognized tokens
- malformed operators
- incomplete expressions
- unclosed blocks
- unclosed cycles
- invalid attribute assignments
- invalid dimension tokens
Errors must include:
- line number
- token or operator causing failure
- expected vs. received structure

9. Parsing Output Format
The parser outputs a structured AST (Abstract Syntax Tree) with:
- node type
- attributes
- dimensional bindings
- closure states
- tension values
- relations
- block hierarchy
This AST is passed to the evaluation layer.

10. Summary
Parsing Rules define how SLP text is transformed into structured internal form:
- lexing
- expression parsing
- statement parsing
- block parsing
- cycle parsing
- error handling
- AST generation
Parsing is the foundation of the interpreter pipeline.
