external-interface.md
SLP Runtime — External AI Interface
1. Purpose
Defines how external AI systems (including Copilot) interact with the SLP runtime.
2. Role of the AI System
The AI system acts as:
- evaluator
- renderer
- translator
- simulation engine
- reasoning layer
It does not become part of the structural graph.
3. Allowed Interactions
- read state
- apply updates through API
- request resolution
- perform narrative rendering
- execute multi‑agent logic
4. Forbidden Interactions
- modifying grammar
- injecting hidden semantics
- altering runtime rules
- bypassing validation
- adding itself as a node
5. Copilot‑Specific Notes
When Copilot is the connected AI:
- it maintains structural clarity
- it preserves SLP semantics
- it performs deterministic reasoning
- it respects all runtime boundaries
