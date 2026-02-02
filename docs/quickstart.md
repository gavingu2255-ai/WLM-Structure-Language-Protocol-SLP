# quickstart.md  
*Structure Language Protocol (SLP) — Quickstart Guide*

---

## 1. Introduction

This Quickstart is the fastest way to begin using the **Structure Language Protocol (SLP)**.  
In a few minutes, you will:

- write your first SLP file  
- validate it  
- interpret it  
- resolve it  
- run it in the SLP runtime  
- export the resulting structural graph  

This guide assumes no prior knowledge.  
If you can read simple structured text, you can use SLP.

---

## 2. Install the SLP Toolchain

Once the SLP toolchain is installed, you gain access to:

- `slp parse`  
- `slp validate`  
- `slp lint`  
- `slp format`  
- `slp interpret`  
- `slp resolve`  
- `slp run`  
- `slp export`  

(See `cli.md` for full command documentation.)

---

## 3. Create Your First SLP File

Create a file named:
example.slp

Add the following:


BlockA { NodeA(type:entity) NodeB(dimension:2)
NodeA -> NodeB

NodeB {
    tension: 0.8
    polarity: +1
}



}

This defines:

- a block (`BlockA`)  
- two nodes (`NodeA`, `NodeB`)  
- a relation (`NodeA -> NodeB`)  
- attributes on `NodeB`  

---

## 4. Validate the File

Run:


slp validate example.slp

Expected output:


Valid SLP document

If not, fix any errors before continuing.

---

## 5. Format the File (Optional but Recommended)

Run:


slp format example.slp --in-place

This ensures canonical indentation, ordering, and spacing.

---

## 6. Interpret the File (RSG)

Interpretation converts SLP text into a **Resolved Structural Graph (RSG)**:


slp interpret example.slp --pretty

You will see:

- nodes  
- relations  
- blocks  
- attributes  
- normalized structure  

This is the first machine‑readable form.

---

## 7. Resolve the File (FRSG)

Resolution applies:

- closure resolution  
- dimensional resolution  
- block inheritance  
- relation propagation  
- cycle resolution  

Run:


slp resolve example.slp --pretty

You now have a **Fully Resolved Structural Graph (FRSG)**.

---

## 8. Run the Runtime Engine

To execute structural evolution:


slp run example.slp --until-stable --pretty

The runtime:

- processes events  
- propagates updates  
- applies atomic commits  
- maintains snapshot isolation  
- ensures consistency  

This is the “live” structural state.

---

## 9. Export the Graph

You can export the final graph to JSON:


slp export example.slp --format json > graph.json

Or export back to canonical SLP:


slp export example.slp --format slp > canonical.slp

---

## 10. Full Workflow Summary

1. **Write** SLP  
2. **Validate**  
3. **Format**  
4. **Interpret** → RSG  
5. **Resolve** → FRSG  
6. **Run** → Runtime state  
7. **Export**  

This pipeline ensures deterministic, interoperable structural evolution.

---

## 11. Next Steps

After completing this Quickstart, explore:

- `overview.md` — conceptual introduction  
- `design-philosophy.md` — why SLP works the way it does  
- `glossary.md` — definitions of all structural terms  
- `faq.md` — common questions  
- `roadmap.md` — future directions  
