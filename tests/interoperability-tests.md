# interoperability-tests.md  
*Structure Language Protocol (SLP) — Interoperability Test Suite*

---

## 1. Purpose

Interoperability tests verify that SLP:

- behaves consistently across different interpreters  
- produces identical RSG/FRSG outputs across implementations  
- maintains structural integrity across tools (formatter, validator, linter, CLI)  
- supports round‑trip transformations without loss  
- integrates safely with external systems (including AI executors)  
- preserves determinism across environments  

These tests ensure SLP functions as a **cross‑platform, cross‑implementation protocol**.

Interoperability tests run **after runtime tests** and represent the final verification layer before public release.

---

## 2. Test Categories

Interoperability tests are grouped into:

1. **Cross‑Interpreter Consistency Tests**  
2. **Round‑Trip Stability Tests**  
3. **Toolchain Interoperability Tests**  
4. **External System Integration Tests**  
5. **AI Executor Interoperability Tests**  
6. **Cross‑Version Compatibility Tests**  
7. **Invalid Interoperability Tests**

Each category ensures SLP behaves identically across environments.

---

## 3. Cross‑Interpreter Consistency Tests

### 3.1 Identical RSG Output Across Interpreters

Input:
NodeA NodeB NodeA -> NodeB

Expected:
- All interpreters produce identical RSG  
- Node IDs, relation IDs, and block structure match exactly  

### 3.2 Attribute Consistency

Input:


NodeA { tension: 0.5 polarity: +1 }

Expected:
- All interpreters produce identical attribute sets  

### 3.3 Block Consistency

Input:


BlockA { NodeA }

Expected:
- Block hierarchy identical across implementations  

---

## 4. Round‑Trip Stability Tests

### 4.1 Parse → Format → Parse

Input:


NodeA { tension: 0.5 }

Process:
1. Parse to RSG  
2. Format to SLP text  
3. Parse again  

Expected:
- Final RSG identical to initial RSG  

### 4.2 Parse → Lint → Parse

Input:


NodeA NodeB NodeA -> NodeB

Expected:
- Linter does not alter semantics  
- Final RSG identical  

### 4.3 Parse → Validate → Format → Parse

Expected:
- No structural drift  
- No attribute loss  
- No relation reordering  

---

## 5. Toolchain Interoperability Tests

### 5.1 Formatter + Validator

Input:


BlockA { NodeA }

Process:
- Formatter normalizes indentation  
- Validator checks structure  

Expected:
- Valid SLP  
- No semantic changes  

### 5.2 Linter + Interpreter

Input:


NodeA(type:entity)

Expected:
- Linter suggestions do not change meaning  
- Interpreter output identical  

### 5.3 CLI → Runtime → CLI

Process:
- CLI loads file  
- Runtime executes  
- CLI exports updated graph  

Expected:
- Exported graph matches runtime state  

---

## 6. External System Integration Tests

### 6.1 JSON Export Consistency

Input:


NodeA NodeB A -> B

Process:
- Export RSG to JSON  
- Import JSON into another implementation  

Expected:
- Identical FRSG  

### 6.2 API Round‑Trip

Process:
- Create nodes via API  
- Query graph  
- Export to SLP  
- Re‑import  

Expected:
- No structural drift  

### 6.3 External Tool Compatibility

Input:
- Graph exported to external visualization tool  

Expected:
- Node/edge structure preserved  
- No attribute loss  

---

## 7. AI Executor Interoperability Tests

### 7.1 AI Reads Snapshot Correctly

Graph:


NodeA { tension: 0.5 }

AI Action:
- Query snapshot  

Expected:
- AI receives correct read‑only state  

### 7.2 AI Proposes Update via API

AI Action:


set_attribute(NodeA, tension=0.8)

Expected:
- Runtime processes event  
- AI cannot bypass validation  
- Final tension = 0.8  

### 7.3 AI Cannot Mutate Memory Directly

Attempt:
- AI tries to modify internal memory  

Expected:
- API error  
- No state change  

### 7.4 AI Round‑Trip Structural Reasoning

Process:
- AI reads graph  
- AI proposes structural update  
- Runtime applies update  
- AI re‑reads graph  

Expected:
- Consistent state across all steps  

---

## 8. Cross‑Version Compatibility Tests

### 8.1 Forward Compatibility

SLP v1 document loaded into SLP v2 interpreter.

Expected:
- Valid  
- No semantic drift  
- Deprecated features flagged but preserved  

### 8.2 Backward Compatibility

SLP v2 document exported to SLP v1 mode.

Expected:
- Compatible subset preserved  
- Unsupported features removed safely  

### 8.3 Runtime Version Drift

Runtime v1 and v2 execute same RSG.

Expected:
- Identical FRSG  
- Identical propagation behavior  

---

## 9. Invalid Interoperability Tests

### 9.1 Divergent Interpreter Output

Two interpreters produce different RSGs.

Expected:
- Interoperability error  
- Test fails  

### 9.2 Formatter Introduces Drift

Formatter output changes semantics.

Expected:
- Interoperability error  

### 9.3 AI Attempts Hidden State Injection

Expected:
- API violation error  
- No commit  

---

## 10. Summary

This test suite verifies that SLP:

- behaves identically across interpreters and runtimes  
- supports stable round‑trip transformations  
- integrates cleanly with tools and external systems  
- interacts safely with AI executors  
- maintains cross‑version compatibility  
- prevents semantic drift  

Interoperability tests ensure SLP functions as a **true protocol**, not just an implementation.



