[![Learning Path](https://img.shields.io/badge/Learning_Path-Free_First-1e90ff?style=for-the-badge)](#)
[![Stack](https://img.shields.io/badge/Stack-Ollama_|_HF_Transformers_|_FAISS_|_LM_Studio-00b894?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-MIT-2d3436?style=for-the-badge)](#)

# Free Prompt Engineering & LLM Systems — No-Cost Playbook

A hands-on path to practice prompt patterns, chaining, evals, and simple tool use **without** paying for the OpenAI platform. Mirrors the structure of popular short courses on prompt engineering and system design, adapted for **local or free resources**.

---

## 📚 Table of Contents

* [What You’ll Build](#what-youll-build)
* [Quick Start (10 minutes)](#quick-start-10-minutes)
* [Environment Setup](#environment-setup)
* [Course-Mirrored Steps (Free Alternatives)](#course-mirrored-steps-free-alternatives)

  * [1) Prompt Fundamentals](#1-prompt-fundamentals)
  * [2) Chaining Calls (Systems)](#2-chaining-calls-systems)
  * [3) Structured Output & JSON “Function Calling”](#3-structured-output--json-function-calling)
  * [4) Retrieval-Augmented Generation (RAG)](#4-retrieval-augmented-generation-rag)
  * [5) Safety & Simple Evaluations](#5-safety--simple-evaluations)
* [Mermaid Workflow](#mermaid-workflow)
* [Exercises & Checkpoints](#exercises--checkpoints)
* [Troubleshooting](#troubleshooting)
* [Attribution](#attribution)

---

## What You’ll Build

* A **local LLM lab** using free tools
* Reusable **prompt templates**
* A **pipeline** that chains steps (Analyze ➜ Plan ➜ Generate)
* A minimal **RAG** demo with a local vector index
* Basic **evals/sanity checks**

---

## Quick Start (10 minutes)

1. **Install Ollama**: [https://ollama.com](https://ollama.com)
2. Pull a small model:

   ```bash
   ollama pull mistral:7b
   ```
3. Chat locally:

   ```bash
   ollama run mistral:7b
   ```
4. Optional GUI: **LM Studio** (point it at an open model and play).

---

## Environment Setup

**Option A: Local + Python**

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install transformers torch datasets faiss-cpu sentence-transformers jupyter
```

**Option B: Google Colab (Free)**
Use `transformers` pipelines directly in a notebook (no GPU required for small models).

**Optional enhancements**

* `langchain` or `llama-index` for chaining
* `datasets` for small eval sets
* `faiss-cpu` for RAG

---

## Course-Mirrored Steps (Free Alternatives)

### 1) Prompt Fundamentals

**Do it free**

* Create `prompts/base.txt` with: **Task**, **Constraints** (tone, audience, style), **Context** (delimited), **Examples** (1–3).
* Run with a local model (Ollama or `transformers`) and iterate until outputs meet spec.

### 2) Chaining Calls (Systems)

**Do it free**

* **Step A (Analyze)** → extract key points
* **Step B (Plan)** → outline as JSON
* **Step C (Write)** → generate final artifact from the plan
* Glue steps with Python functions that call your local model.

### 3) Structured Output & JSON “Function Calling”

**Do it free**

* Force **strict JSON** output; validate with regex/`jsonschema`; retry on failure.
* Simulate “tools” by:

  * Asking the model for a **JSON plan** (tool + args),
  * Executing the tool in Python,
  * Feeding the **tool result** back to the model.

### 4) Retrieval-Augmented Generation (RAG)

**Do it free**

* Build a tiny FAISS index:

  * Split docs → embed with `sentence-transformers` → store in FAISS
  * Retrieve top-k → include in prompt context
* Return **citations** (source filenames/IDs) with answers.

### 5) Safety & Simple Evaluations

**Do it free**

* Maintain a small CSV of prompts + required properties (e.g., “must include a numbered list”; “no PII”).
* Add a Python checker that flags misses and retries with a corrective system message.

---

## Mermaid Workflow

```mermaid
flowchart LR
  %% === LAYERS / STAGES ======================================================
  subgraph INPUT["User Interaction Layer"]
    A1([User Request])
    A2([Uploaded Docs / Data])
  end

  subgraph PREPROC["Input Governance & Parsing"]
    B1{{Guardrails: Policy / Security / PII}}
    B2([Language & Format Normalization])
  end

  subgraph CONTEXT["Context & Knowledge Injection"]
    C1[(Vector Store: FAISS)]
    C2([Top-K Retrieval & Ranking])
  end

  subgraph PIPELINE["LLM Processing Pipeline"]
    D1[[Step A: Analysis & Entity Extraction]]
    D2[[Step B: Planning (Strict JSON Schema)]]
    D3[[Step C: Tool Invocation / External APIs]]
    D4[[Step D: Draft Generation]]
  end

  subgraph EVAL["Validation & Quality Gates"]
    E1{{Spec Compliance / JSON Validity}}
    E2{{Safety Filters / Hallucination Checks}}
  end

  subgraph OUTPUT["Delivery & Feedback"]
    F1([Formatted Output])
    F2([Citations / Sources])
    F3([Feedback Loop to User])
  end

  %% === FLOWS ================================================================
  A1 --> B1 --> B2
  A2 --> B2
  B2 -->|valid| C1 --> C2
  C2 --> D1 --> D2 --> D3 --> D4 --> E1
  E1 -->|pass| F1 --> F2 --> F3
  E1 -->|fail| D2
  E2 -. optional audits .-> E1

  %% === STYLE CLASSES ========================================================
  classDef process fill:#1e90ff,stroke:#0d3b66,color:#ffffff,stroke-width:2px
  classDef decision fill:#f39c12,stroke:#874000,color:#ffffff,stroke-width:2px
  classDef data fill:#27ae60,stroke:#0b3d2e,color:#ffffff,stroke-width:2px
  classDef output fill:#34495e,stroke:#1f2a35,color:#ffffff,stroke-width:2px

  class A1,A2,F1,F2,F3 process
  class B1,E1,E2 decision
  class C1,C2 data
  class D1,D2,D3,D4 process
  class F1,F2,F3 output
```

---

## Exercises & Checkpoints

* **Prompt tuning:** add/remove constraints and compare outputs.
* **Chain growth:** add a *review* step enforcing a style guide.
* **RAG:** index your course notes and cite 2–3 sources per answer.
* **Eval:** write 10 tests; aim for ≥80% pass rate before you “ship”.

---

## Troubleshooting

* **Outputs off-spec:** add explicit formatting constraints and a minimal example.
* **JSON keeps breaking:** prepend a schema, validate, and retry with the validation error.
* **Slow on CPU:** use smaller models (3–7B) and reduce context length.

---

## Attribution

This README mirrors course-style principles using **free/local tools** so you can build skills without API spend.

---

### Quick tips if it still doesn’t render

* Do **not** wrap the entire README inside a triple-backtick code fence.
* Ensure the Mermaid block is exactly like above:

  * A blank line before ` ```mermaid `
  * No leading spaces or `>` quotes on that line
  * A matching closing triple backtick on its own line
* GitHub renders Mermaid in repos, gists, and PR descriptions; some editors (e.g., Discord/Notion) may require a Mermaid plugin or won’t render it natively.


