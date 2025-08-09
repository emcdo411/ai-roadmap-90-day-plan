[![Learning Path](https://img.shields.io/badge/Learning_Path-Free_First-1e90ff?style=for-the-badge)](#)
[![Stack](https://img.shields.io/badge/Stack-Ollama_|_HF_Transformers_|_FAISS_|_LM_Studio-00b894?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-MIT-2d3436?style=for-the-badge)](#)

# Free Prompt Engineering & LLM Systems — No-Cost Playbook

A hands-on path to practice **deeplearning.ai** course principles (prompt patterns, chaining, evals, and simple tool use) without paying for the OpenAI platform. Mirrors the structure of the short courses “ChatGPT Prompt Engineering for Developers” and “Building Systems with the ChatGPT API,” adapted for **local or free resources**.

---

## 📚 Table of Contents
- [What You’ll Build](#what-youll-build)
- [Quick Start (10 minutes)](#quick-start-10-minutes)
- [Environment Setup](#environment-setup)
- [Course-Mirrored Steps (Free Alternatives)](#course-mirrored-steps-free-alternatives)
  - [1) Prompt Fundamentals](#1-prompt-fundamentals)
  - [2) Chaining Calls (Systems)](#2-chaining-calls-systems)
  - [3) Structured Output & JSON “Function Calling”](#3-structured-output--json-function-calling)
  - [4) Retrieval-Augmented Generation (RAG)](#4-retrieval-augmented-generation-rag)
  - [5) Safety & Simple Evaluations](#5-safety--simple-evaluations)
- [Mermaid Workflow](#mermaid-workflow)
- [Exercises & Checkpoints](#exercises--checkpoints)
- [Troubleshooting](#troubleshooting)
- [Attribution](#attribution)

---

## What You’ll Build
- A **local LLM lab** using free tools
- Reusable **prompt templates**
- A **pipeline** chaining steps (Analyze ➜ Plan ➜ Generate)
- A **RAG** demo with a local vector index
- Basic **evals/sanity checks**

---

## Quick Start (10 minutes)
1. **Install Ollama**: https://ollama.com  
2. Pull a small model:
   ```bash
   ollama pull mistral:7b
````

3. Chat locally:

   ```bash
   ollama run mistral:7b
   ```
4. Optional GUI: **LM Studio** for a point-and-click experience.

---

## Environment Setup

**Option A: Local + Python**

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install transformers torch datasets faiss-cpu sentence-transformers jupyter
```

**Option B: Google Colab (Free)**
Use `transformers` pipelines directly in Colab (no GPU required for small models).

**Optional Enhancements:**

* `langchain` or `llama-index` for chaining
* `datasets` for small eval sets
* `faiss-cpu` for RAG

---

## Course-Mirrored Steps (Free Alternatives)

### 1) Prompt Fundamentals

**Do it free:**

* Create `prompts/base.txt` with **Task**, **Constraints**, **Context**, and **Examples**.
* Run with a local model (Ollama or `transformers`).

### 2) Chaining Calls (Systems)

**Do it free:**

* Step A: Analyze → Step B: Plan (JSON) → Step C: Write.
* Glue with Python functions calling local LLM.

### 3) Structured Output & JSON “Function Calling”

**Do it free:**

* Force JSON output with schema checks; retry if invalid.
* Simulate tool calls via JSON plans → Python executes → feed results back.

### 4) Retrieval-Augmented Generation (RAG)

**Do it free:**

* Build FAISS index: split docs → embed → store → retrieve top-k → append to prompt.
* Include **citations** with results.

### 5) Safety & Simple Evaluations

**Do it free:**

* CSV of prompts + expected rules.
* Python checker flags failures, retries with corrective prompt.

---

## Mermaid Workflow

```mermaid
flowchart LR
  subgraph INPUT[User Interaction Layer]
    A1([User Request])
    A2([Uploaded Docs / Data])
  end

  subgraph PREPROC[Input Governance & Parsing]
    B1{{Guardrails: Policy / Security Checks}}
    B2([Language & Format Normalization])
  end

  subgraph CONTEXT[Context & Knowledge Injection]
    C1[(Vector Store: FAISS)]
    C2([Context Retrieval & Ranking])
  end

  subgraph PIPELINE[LLM Processing Pipeline]
    D1[[Step A: Analysis & Entity Extraction]]
    D2[[Step B: Planning (JSON Schema)]]
    D3[[Step C: Tool Invocation / External API Calls]]
    D4[[Step D: Draft Generation]]
  end

  subgraph EVAL[Validation & Quality Gates]
    E1{{Spec Compliance Checks}}
    E2{{Safety Filters & PII Scan}}
  end

  subgraph OUTPUT[Delivery Layer]
    F1([Formatted Output])
    F2([Citations / References])
    F3([Feedback Loop to User])
  end

  %% Connections
  A1 --> B1 --> B2
  A2 --> B2
  B2 -->|Valid| C1 --> C2
  C2 --> D1 --> D2 --> D3 --> D4 --> E1
  E1 -->|Pass| F1
  E1 -->|Fail| D2
  F1 --> F2 --> F3

  %% Styling
  classDef process fill=#1e90ff,stroke=#0d3b66,color=#fff,stroke-width=2px
  classDef decision fill=#f39c12,stroke=#874000,color=#fff,stroke-width=2px
  classDef data fill=#27ae60,stroke=#0b3d2e,color=#fff,stroke-width=2px

  class A1,A2,F1,F2,F3 process
  class B1,E1,E2 decision
  class C1,C2 data
  class D1,D2,D3,D4 process
```

This diagram:

* **Shows swimlane-like stages** for a clear enterprise architecture narrative.
* **Separates governance, context retrieval, LLM processing, and output delivery** like a Deloitte/AWS architecture deck.
* Uses **clear conditional flow** and **loop-backs for quality gates**.

---

## Exercises & Checkpoints

* Tune prompts by adding/removing constraints.
* Add a review step enforcing a style guide.
* Build a RAG index from your notes, return top-3 sources.
* Write 10 eval tests, target ≥80% pass before shipping.

---

## Troubleshooting

* **Off-spec output:** tighten formatting constraints + add minimal examples.
* **Broken JSON:** use schema validation + retry loop.
* **Slow CPU:** smaller model (3–7B), shorter context.

---

## Attribution

This README mirrors **deeplearning.ai** course principles but uses **free/local tools** so you can train without API spend.

```

---

If you want, I can now also **add an AWS-style architecture diagram** (boxes + services icons) as a secondary visual below the Mermaid for a real *boardroom deliverable*. That would give you a dual-view: **process workflow** + **system architecture**.  

Do you want me to add that as well?
```

