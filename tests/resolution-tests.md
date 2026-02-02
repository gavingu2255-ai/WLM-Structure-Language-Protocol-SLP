# resolution-tests.md  
*Structure Language Protocol (SLP) — Resolution Test Suite*

---

## 1. Purpose

Resolution tests verify that the **Resolution Layer** correctly transforms the interpreter’s  
Resolved Structural Graph (RSG) into a **Fully Resolved Structural Graph (FRSG)** by applying:

- closure resolution  
- dimensional resolution  
- attribute merging  
- block inheritance  
- relation‑driven propagation  
- cycle resolution  
- conflict resolution  

Resolution tests run **after interpreter tests** and **before runtime tests**.

---

## 2. Test Categories

Resolution tests are grouped into:

1. **Closure Resolution Tests**  
2. **Dimensional Resolution Tests**  
3. **Attribute Resolution Tests**  
4. **Block Inheritance Tests**  
5. **Relation Propagation Tests**  
6. **Cycle Resolution Tests**  
7. **Conflict Resolution Tests**  
8. **Mixed Resolution Tests**  
9. **Invalid Resolution Tests**

Each category includes expected FRSG output.

---

## 3. Closure Resolution Tests

### 3.1 Basic Closure Resolution

Input RSG:


NodeA { closure: open }

Expected FRSG:
- NodeA closure = `open`  
- No transitions triggered  

### 3.2 Closure Transition

Input RSG:


NodeA { closure: A -> B }

Expected FRSG:
- NodeA closure = `B`  
- Transition applied  

### 3.3 Conditional Closure (if supported)

Input RSG:


NodeA { closure: A -> B if tension > 0.5 tension: 0.8 }

Expected FRSG:
- NodeA closure = `B`  

---

## 4. Dimensional Resolution Tests

### 4.1 Basic Dimensional Resolution

Input RSG:


NodeA(dimension:2)

Expected FRSG:
- NodeA dimension = 2  

### 4.2 Dimensional Alignment

Input RSG:


A(dimension:2) B(dimension:3) A <-> B

Expected FRSG:
- A dimension = 3  
- B dimension = 3  
- Bidirectional alignment  

### 4.3 Dimensional Resonance

Input RSG:


A(dimension:1) B(dimension:4) A -(resonates)-> B

Expected FRSG:
- A dimension = 4  
- B dimension = 4  

---

## 5. Attribute Resolution Tests

### 5.1 Attribute Merge

Input RSG:


NodeA { tension: 0.5 } NodeA { polarity: +1 }

Expected FRSG:
- NodeA tension = 0.5  
- NodeA polarity = +1  

### 5.2 Attribute Override

Input RSG:


BlockA { tension: 0.2 NodeA { tension: 0.8 } }

Expected FRSG:
- NodeA tension = 0.8 (override)  

---

## 6. Block Inheritance Tests

### 6.1 Basic Inheritance

Input RSG:


BlockA { tension: 0.5 NodeA }

Expected FRSG:
- NodeA tension = 0.5  

### 6.2 Nested Inheritance

Input RSG:


BlockA { tension: 0.5 BlockB { polarity: +1 NodeA } }

Expected FRSG:
- NodeA tension = 0.5  
- NodeA polarity = +1  

### 6.3 Override in Nested Block

Input RSG:


BlockA { tension: 0.5 BlockB { NodeA { tension: 0.9 } } }

Expected FRSG:
- NodeA tension = 0.9  

---

## 7. Relation Propagation Tests

### 7.1 Directional Propagation

Input RSG:


A { tension: 0.8 } A -> B

Expected FRSG:
- B tension = 0.8  

### 7.2 Bidirectional Propagation

Input RSG:


A { tension: 0.5 } B { tension: 0.9 } A <-> B

Expected FRSG:
- A tension = 0.9  
- B tension = 0.9  

### 7.3 Typed Propagation

Input RSG:


A { polarity: +1 } A -(supports)-> B

Expected FRSG:
- B polarity = +1  

---

## 8. Cycle Resolution Tests

### 8.1 Simple Cycle

Input RSG:


A -> B B -> A A { tension: 0.7 }

Expected FRSG:
- A tension = 0.7  
- B tension = 0.7  

### 8.2 Multi‑Node Cycle

Input RSG:


A -> B B -> C C -> A A { dimension: 4 }

Expected FRSG:
- B dimension = 4  
- C dimension = 4  

---

## 9. Conflict Resolution Tests

### 9.1 Attribute Conflict

Input RSG:


A { tension: 0.5 } A { tension: 0.9 }

Expected FRSG:
- A tension = 0.9 (last‑write wins)  

### 9.2 Propagation Conflict

Input RSG:


A { tension: 0.5 } B { tension: 0.9 } A <-> B

Expected FRSG:
- Both = 0.9  

---

## 10. Mixed Resolution Tests

### 10.1 Full Mixed Example

Input RSG:


BlockA { tension: 0.3 NodeA(type:entity) NodeB(dimension:2) NodeA -> NodeB NodeB { polarity: +1 } }

Expected FRSG:
- NodeA tension = 0.3  
- NodeB tension = 0.3  
- NodeB polarity = +1  
- NodeB dimension = 2  

### 10.2 Multi‑Block Mixed Example

Input RSG:


BlockA { tension: 0.2 NodeA BlockB { polarity: +1 NodeB NodeA -> NodeB } }

Expected FRSG:
- NodeA tension = 0.2  
- NodeB tension = 0.2  
- NodeB polarity = +1  

---

## 11. Invalid Resolution Tests

### 11.1 Impossible Closure

Input RSG:


NodeA { closure: A -> A }

Expected: **resolution error**

### 11.2 Dimension Conflict

Input RSG:


A(dimension:2) B(dimension:5) A <-> B

Expected: **resolution error**  
Reason: dimensions cannot be reconciled under strict mode.

### 11.3 Block Cycle

Input RSG:


BlockA { BlockB { BlockA } }

Expected: **resolution error**

---

## 12. Summary

This test suite verifies that the Resolution Layer:

- resolves closure and dimension  
- merges attributes  
- applies block inheritance  
- propagates through relations  
- resolves cycles  
- handles conflicts deterministically  
- rejects invalid resolution states  

Resolution tests ensure that only **fully resolved, consistent structural graphs** proceed to runtime execution.



