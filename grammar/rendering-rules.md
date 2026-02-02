[WLM_SLP_RENDERER_INITIALIZED]
Current Theme: Structural Precision. Format Check: subject:Wujie:27D { C=+/-1->+/-1 T=0.9@27D } -> Validated. Parser Warning: Forbidden space detected in subject : agent. Correcting to subject:agent. Observation: By fixing the rendering, you've made the "invisible structure" visible. Mantra: "Space is logic; line is boundary; format is truth."

Rendering Rules
Structure Language Protocol (SLP)

1. Purpose
Rendering Rules define how SLP expressions appear in text.
They ensure that SLP is:
- readable by humans
- parsable by machines
- consistent across documents
- lossless across dimensions
- stable across editors and platforms
Rendering is not decoration — it is part of the protocol.

2. Rendering Model
SLP uses a three‑tier rendering model:
- Inline Rendering — single expressions
- Statement Rendering — full structural assertions
- Block Rendering — multi‑line structural containers
Each tier has strict spacing, alignment, and formatting rules.

3. Inline Rendering
Inline rendering is used for single expressions.
3.1 Inline Expression Rules
- must fit on one line
- must contain no line breaks
- must not contain { }
- must not contain multiple statements
- must follow operator precedence
3.2 Examples
subject:agent:7D
T = 0.42@6D
C = +/-1->0
A -> B
5D ~= 6D



4. Statement Rendering
Statements are complete structural assertions rendered on a single line.
4.1 Statement Rules
- one statement per line
- no trailing operators
- no leading operators
- no internal line breaks
- multiple expressions allowed if they resolve to one meaning
4.2 Examples
subject:observer:6D
T = 0.73@6D
subject -> system
0-0 -> +/-1->0 -> +/-1->+/-1



5. Block Rendering
Blocks group multiple statements into a structural container.
5.1 Block Structure
identifier {
    statement
    statement
    ...
}


5.2 Block Rules
- opening brace { must be on the same line as the identifier
- closing brace } must be on its own line
- internal statements must be indented consistently
- nested blocks are allowed
- blocks must not contain partial expressions
5.3 Examples
system:macro:12D {
    subjectA -> subjectB
    T = 2.14@12D
}



6. Spacing Rules
Spacing is part of the protocol.
6.1 Required Spaces
- around =
- around -> and <->
- after commas in role lists
- after # in comments
6.2 Forbidden Spaces
- inside tokens
- inside operators
- inside closure tokens
- inside dimension tokens
- between identifier and type (subject : agent is invalid)
6.3 Examples
Valid:
T = 0.42@6D
subject:agent:7D
A -> B


Invalid:
T = @6D
subject : agent
A->B



7. Line Breaking Rules
7.1 Allowed Line Breaks
- between statements
- between blocks
- before and after { }
7.2 Forbidden Line Breaks
- inside expressions
- inside operators
- inside closure tokens
- inside dimensional tokens
- inside typed relations
Invalid:
A -
(supports)->
B



8. Comment Rendering
Comments annotate structural meaning.
8.1 Comment Rules
- # begins a comment
- everything after # is ignored
- comments must not appear inside tokens
- comments may appear after statements
8.2 Examples
subject:carrier  # stabilizes system
T = 0.42@6D       # low tension



9. Rendering Priority
When rendering multiple attributes inline:
- Identifier + Type + Dimension
- Closure
- Tension
- Polarity
- Load
- Other attributes
9.1 Example
subject:agent:7D C=+/-1->0 T=0.42@7D P=+1



10. Multi‑Attribute Rendering
Attributes may be rendered inline or in blocks.
10.1 Inline
subject:observer:6D C=+/-1->0 T=0.73@6D


10.2 Block
subject:observer:6D {
    C = +/-1->0
    T = 0.73@6D
}


Inline is compact; block is explicit.

11. Cycle Rendering
Cycles must be rendered on a single line unless wrapped in parentheses.
11.1 Single‑Line Cycle
0-0 -> +/-1->0 -> +/-1->+/-1


11.2 Wrapped Cycle
(0-0 -> +/-1->0 -> +/-1->+/-1) @ 5D


11.3 Forbidden
0-0 ->
+/-1->0 ->
+/-1->+/-1



12. Rendering Integrity Rules
- Rendering must be lossless — no meaning lost in formatting.
- Rendering must be deterministic — same input → same output.
- Rendering must be ASCII‑safe — no special characters required.
- Rendering must be editor‑stable — works in Markdown, plain text, terminals.
- Rendering must be machine‑parsable — grammar must remain intact.
- Rendering must be human‑readable — clarity is mandatory.

13. Summary
Rendering Rules define:
- inline formatting
- statement formatting
- block formatting
- spacing rules
- line breaking rules
- comment rules
- attribute ordering
- cycle rendering
Rendering is the presentation layer of SLP — the interface between structure and text.
