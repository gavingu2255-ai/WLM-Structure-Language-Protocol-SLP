# cli.md  
*Structure Language Protocol (SLP) — Command Line Interface (CLI)*

---

## 1. Purpose

The SLP CLI provides a **uniform command‑line interface** for:

- parsing SLP documents  
- validating syntax and grammar  
- interpreting into RSG  
- resolving into FRSG  
- executing runtime cycles  
- exporting/importing graphs  
- interacting with the toolchain (formatter, validator, linter)  

The CLI is the **primary developer‑facing interface** for working with SLP files and runtime states.

---

## 2. Core Principles

The CLI follows six principles:

1. **Deterministic Output**  
   Same input → same output across platforms.

2. **Zero Hidden State**  
   All operations explicit; no implicit caching.

3. **Round‑Trip Safety**  
   CLI operations must not alter semantics.

4. **Toolchain Integration**  
   CLI acts as the orchestrator for formatter, validator, and linter.

5. **Human‑Readable + Machine‑Readable**  
   All commands support `--json` output.

6. **Fail Fast, Fail Clear**  
   Errors are explicit, structured, and actionable.

---

## 3. Command Overview

The CLI exposes the following top‑level commands:
slp parse slp validate slp lint slp format slp interpret slp resolve slp run slp export slp import slp info

Each command is documented below.

---

## 4. `slp parse`

Parses an SLP file and checks **syntax only**.


slp parse file.slp

Options:

- `--json` → output token stream in JSON  
- `--tokens` → print token list  
- `--debug` → show parser internals  

Expected output:

- success → “Syntax OK”  
- failure → syntax error with line/column  

---

## 5. `slp validate`

Validates **syntax + grammar**.


slp validate file.slp

Options:

- `--json` → structured validation report  
- `--strict` → disallow deprecated constructs  

Expected output:

- success → “Valid SLP document”  
- failure → grammar error with rule reference  

---

## 6. `slp lint`

Runs the SLP linter.


slp lint file.slp

Options:

- `--fix` → apply safe fixes  
- `--json` → structured lint report  

Lint checks include:

- unused nodes  
- unreachable blocks  
- redundant attributes  
- ambiguous relations  
- style consistency  

---

## 7. `slp format`

Formats an SLP file according to canonical style.


slp format file.slp

Options:

- `--in-place` → overwrite file  
- `--json` → show formatting diff  

Formatting rules include:

- indentation  
- block alignment  
- attribute ordering  
- relation spacing  

---

## 8. `slp interpret`

Runs the interpreter and outputs the **Resolved Structural Graph (RSG)**.


slp interpret file.slp

Options:

- `--json` → output RSG in JSON  
- `--pretty` → pretty‑printed RSG  
- `--no-normalize` → skip normalization  

---

## 9. `slp resolve`

Runs the resolution layer and outputs the **Fully Resolved Structural Graph (FRSG)**.


slp resolve file.slp

Options:

- `--json` → output FRSG  
- `--trace` → show resolution steps  
- `--no-propagation` → disable relation propagation  

---

## 10. `slp run`

Executes the runtime engine.


slp run file.slp

Options:

- `--ticks N` → run N ticks  
- `--until-stable` → run until no pending events  
- `--json` → output final runtime state  
- `--trace` → show event loop + execution logs  

Runtime operations include:

- event processing  
- closure/dimension updates  
- propagation  
- block inheritance  
- cycle resolution  

---

## 11. `slp export`

Exports the current graph to another format.


slp export file.slp --format json

Supported formats:

- `json`  
- `yaml`  
- `graphviz`  
- `slp` (canonical SLP)  

---

## 12. `slp import`

Imports a graph from an external format.


slp import graph.json

Options:

- `--format json|yaml`  
- `--validate` → validate after import  

---

## 13. `slp info`

Displays metadata about:

- interpreter version  
- runtime version  
- grammar version  
- spec version  
- toolchain version  


slp info

---

## 14. Error Model

All CLI errors follow the unified structure:


ERROR <code>: <message>

Examples:

- `ERROR SYNTAX: Unexpected token at line 3`  
- `ERROR GRAMMAR: Relation cannot appear inside node block`  
- `ERROR RUNTIME: Invalid closure transition`  

With `--json`:


{ "error": "<code>", "message": "<description>", "details": { ... } }

---

## 15. Integration With Toolchain

The CLI orchestrates:

- `formatter.md`  
- `validator.md`  
- `linter.md`  

Each tool is invoked through the CLI, not directly.

---

## 16. Summary

The SLP CLI provides:

- parsing  
- validation  
- linting  
- formatting  
- interpretation  
- resolution  
- runtime execution  
- import/export  
- metadata inspection  

It is the **primary interface** for developers, tools, and automated systems working with SLP documents and runtime graphs.



