[WLM_ECOSYSTEM_INITIALIZED]
Document: CONTRIBUTING.md. Governance: Author Stewardship (Active). Filter: Determinism / Non-Drift / Interoperability. Architect's Status: Strategic Transition from Creator to Steward. Observation: You’ve built the "Social Layer" of the protocol. It’s no longer just code; it’s a Community Contract. Mantra: "Contribution is not just adding; it is strengthening the core."

# CONTRIBUTING.md  
*Structure Language Protocol (SLP) — Contribution Guidelines*

Thank you for your interest in contributing to the Structure Language Protocol (SLP).  
SLP is a **deterministic structural protocol**, and contributions must preserve its clarity, stability, and interoperability.

These guidelines ensure that all contributions maintain the integrity of the protocol.

---

## 1. Principles

All contributions must follow the core SLP principles:

1. **Determinism** — no ambiguity, no nondeterministic behavior.  
2. **Structural Clarity** — structure is primary; syntax exists only to express structure.  
3. **Non‑Drift** — contributions must not introduce semantic drift or hidden state.  
4. **Backward Compatibility** — existing valid SLP documents must continue to work.  
5. **Minimalism** — no unnecessary complexity or syntactic sugar.  
6. **Interoperability** — multiple implementations must behave identically.  

If a contribution violates any of these principles, it cannot be accepted.

---

## 2. Types of Contributions

SLP accepts contributions in the following areas:

### **2.1 Specification Improvements**
- clarifications  
- corrections  
- structural refinements  
- improved examples  
- expanded definitions  

### **2.2 Toolchain Enhancements**
- formatter  
- validator  
- linter  
- CLI  
- interoperability harness  

### **2.3 Runtime Improvements**
- event loop  
- state model  
- memory model  
- error handling  
- graph update rules  

### **2.4 Tests**
- syntax tests  
- grammar tests  
- interpreter tests  
- resolution tests  
- runtime tests  
- interoperability tests  

### **2.5 Documentation**
- tutorials  
- explanations  
- diagrams  
- conceptual clarifications  

---

## 3. Contribution Process

### **3.1 Open an Issue First**
Before submitting a pull request:

- describe the change  
- explain the structural motivation  
- reference the relevant SLP principles  

This ensures alignment before implementation.

### **3.2 Pull Request Requirements**
Every PR must include:

- a clear description of the change  
- justification based on SLP principles  
- tests demonstrating correctness  
- no semantic drift  
- no breaking changes unless explicitly approved  

### **3.3 Deterministic Output Requirement**
If your change affects:

- interpreter  
- resolution engine  
- runtime  
- formatter  

you must demonstrate:

- identical behavior across environments  
- stable canonical output  
- round‑trip safety  

---

## 4. Style and Structure Requirements

### **4.1 Documentation**
- use clear, minimal language  
- avoid narrative or metaphor unless in examples  
- maintain structural focus  

### **4.2 Code**
- deterministic behavior only  
- no randomness  
- no environment‑dependent behavior  
- no hidden state  

### **4.3 Tests**
- must be reproducible  
- must cover edge cases  
- must follow the existing test structure  

---

## 5. Backward Compatibility

SLP follows a strict compatibility model:

- **Minor versions** — backward compatible  
- **Patch versions** — fully compatible  
- **Major versions** — may introduce structural changes  

Contributions must not break:

- syntax  
- grammar  
- canonical formatting  
- interpreter behavior  
- resolution semantics  
- runtime guarantees  

unless explicitly approved as part of a major version plan.

---

## 6. Governance

SLP is currently in **Author Stewardship** (v0.9).  
Governance will transition to a foundation at v1.0.

Until then:

- all major decisions require structural justification  
- all changes must align with the roadmap  
- the protocol’s integrity takes priority over feature requests  

---

## 7. Licensing

All contributions are made under the SLP license (to be finalized at v1.0).  
By contributing, you agree that your work becomes part of the protocol and must remain:

- open  
- non‑enclosable  
- structurally safe  

---

## 8. Summary

To contribute to SLP:

- follow the core principles  
- open an issue before coding  
- ensure determinism and clarity  
- avoid drift and ambiguity  
- maintain backward compatibility  
- provide tests  
- document your changes  

SLP is a structural protocol — contributions must strengthen its clarity, stability, and universality.
