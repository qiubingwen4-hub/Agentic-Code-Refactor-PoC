# 🤖 Agentic Code Refactor PoC

![Status: Proof of Concept](https://img.shields.io/badge/Status-Proof_of_Concept-yellow)
![Python: 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)
![Architecture: Multi-Agent](https://img.shields.io/badge/Architecture-Multi--Agent-success)

## 📌 Project Overview
**Agentic-Code-Refactor-PoC** is an experimental multi-agent orchestration framework designed to identify, analyze, and automatically refactor deep technical debt in large-scale Python repositories. 

Unlike traditional static analysis tools (like Flake8 or SonarQube) that only catch surface-level syntax issues, this system leverages Abstract Syntax Tree (AST) parsing combined with Large Language Models (LLMs) to understand context, measure cyclomatic complexity, and rewrite poorly structured logic autonomously.

---

## 🚧 Current Status & API Migration Note
> **Note to Reviewers / Sponsors:** > This project is currently in the **Proof of Concept (PoC) phase**. 
> We have successfully validated the core AST scanning and multi-agent self-correction loop on localized modules (see local logs). However, full-repository scanning requires massive context windows (100K+ tokens) and high-concurrency API calls. We are currently bottlenecked by the high costs of existing APIs. 
> 
> **Goal:** We are actively planning to migrate the core reasoning engine to **Xiaomi MiMo models** to leverage its ultra-long context capabilities and cost-effective ecosystem, unlocking the system's full potential for enterprise-level repositories.

---

## ⚙️ Core Architecture (Agent Workflow)

The system operates on a highly decoupled multi-agent pipeline:

1. **AST Global Analyzer Agent (The Brain):**
   - Parses the target directory recursively.
   - Extracts functions, classes, and control flows using Python's native `ast` module.
   - Flags functions with high cyclomatic complexity (e.g., deeply nested `if/for` loops) or excessive line counts.
2. **Refactor & Coder Agent (The Hands):**
   - Receives the JSON-structured debt report.
   - Proposes refactoring strategies (e.g., Extract Method, Strategy Pattern) and rewrites the code block strictly following PEP 8.
3. **Validation & Self-Correction Agent (The Shield):**
   - Automatically generates unit tests for the rewritten code.
   - Catches Terminal logs (`SyntaxError`, `AttributeError`). If a test fails, it feeds the traceback back to the Refactor Agent for an autonomous self-correction loop.

---

## 🗺️ Roadmap
- [x] Implement base AST NodeVisitor for complexity scoring.
- [x] Design multi-agent prompt chaining and role definitions.
- [x] Validate automated Terminal error catching & self-healing loop.
- [ ] **Pending:** Migrate to large-context models (e.g., Xiaomi MiMo) for global file dependency mapping.
- [ ] **Pending:** CI/CD pipeline integration (GitHub Actions).

## 📄 License
MIT License
