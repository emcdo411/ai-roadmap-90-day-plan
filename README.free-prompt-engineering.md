[![Learning Path](https://img.shields.io/badge/Learning_Path-Free_First-1e90ff?style=for-the-badge)](#)
[![Stack](https://img.shields.io/badge/Stack-Ollama_|_HF_Transformers_|_FAISS_|_LM_Studio-00b894?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-MIT-2d3436?style=for-the-badge)](#)

# Free Prompt Engineering & LLM Systems — No-Cost Playbook

A hands-on path to practice **deeplearning.ai** course principles (prompt patterns, chaining, evals, and simple tool use) without paying for the OpenAI platform. Mirrors the structure of the short courses “ChatGPT Prompt Engineering for Developers” and “Building Systems with the ChatGPT API,” adapted for **local or free resources**. :contentReference[oaicite:1]{index=1}

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
- A tiny **pipeline** that chains steps (analyze ➜ transform ➜ generate)
- A minimal **RAG** demo with a local vector index
- Basic **evals/sanity checks**

> This mirrors the skills emphasized in the deeplearning.ai short courses (prompting, chaining, and system design). :contentReference[oaicite:2]{index=2}

---

## Quick Start (10 minutes)
1. **Install Ollama** (runs models locally): https://ollama.com  
2. Pull a small model (quick & light):
   ```bash
   ollama pull mistral:7b
Chat locally:

bash
Copy
Edit
ollama run mistral:7b
Optional GUI: LM Studio (point it at an open model and play).

Environment Setup
Option A: Local + Python

bash
Copy
Edit
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install transformers torch datasets faiss-cpu sentence-transformers jupyter
Option B: Google Colab (free)
Use transformers pipelines directly in a notebook (no GPU required for small models).

Optional: langchain or llama-index to simplify chaining; datasets for small eval sets; faiss-cpu for RAG.

Course-Mirrored Steps (Free Alternatives)
1) Prompt Fundamentals
The course focus: clear instructions, delimiting context, role hints, iterative refinement, few-shot examples. 
DeepLearning.ai

Do it free:

Create prompts/base.txt with:

Task: one sentence

Constraints: bullets (tone, audience, style)

Context: delimited block (---context--- …)

Examples: 1–3 good/weak examples

Run with a local model (Ollama or transformers) and tweak until outputs match your spec.

2) Chaining Calls (Systems)
The course focus: sequence multiple LLM calls + code in between to build workflows. 
DeepLearning.ai

Do it free:

Write a simple Python chain:

Step A (analyze): extract key points

Step B (plan): outline result in bullets

Step C (write): produce the final asset using the outline

Glue with plain Python functions; each step calls your local model (Ollama REST API or transformers).

3) Structured Output & JSON “Function Calling”
The course focus: get structured, machine-usable output; tool use. 
DeepLearning.ai

Do it free:

Prompt the model to return valid JSON only. Add a regex/jsonschema check; if invalid, re-prompt with the error.

For “tools,” simulate by:

Ask model to produce a JSON plan (what tool + arguments).

Your Python executes the tool (e.g., a calculator or web fetch), then feeds the tool result back for the next step.

4) Retrieval-Augmented Generation (RAG)
The course focus: provide external context safely. 
DeepLearning.AI - Learning Platform

Do it free:

Build a tiny FAISS index:

Split docs → embed with sentence-transformers → store vectors in FAISS

Retrieve top-k → concatenate into the prompt context

Keep citations: return source filenames/IDs with each chunk.

5) Safety & Simple Evaluations
The course focus: evaluate inputs/outputs and guardrails. 
DeepLearning.AI - Learning Platform

Do it free:

Create a tiny CSV of prompts + expected properties (e.g., “must include a numbered list”; “no PII”).

Write a Python checker that flags misses, then auto-retries with a corrective system prompt (“You failed constraint X; fix only that.”).

Mermaid Workflow
mermaid
Copy
Edit
flowchart TD
  A[User Input] --> B{Guardrails & Parsing}
  B -->|valid| C[Retrieve Context (FAISS)]
  B -->|invalid| B2[Auto-correct Input]
  C --> D[Step A: Analyze]
  D --> E[Step B: Plan (JSON)]
  E --> F[Tools Runner (Python)]
  F --> G[Step C: Generate]
  G --> H{Eval Checks}
  H -->|pass| I[Final Output]
  H -->|fail| E
Exercises & Checkpoints
Prompt tuning: add/remove constraints; compare outputs

Chain growth: add a review step that enforces a style guide

RAG: index your course notes and cite 2–3 sources per answer

Eval: write 10 tests; aim for ≥80% pass rate before you “ship”

Troubleshooting
Outputs are off-spec: add explicit formatting constraints and one minimal example

JSON keeps breaking: prepend a schema and a validator; return only JSON

Slow on CPU: switch to smaller models (e.g., 3–7B), reduce context length

Attribution
This README mirrors the structure of deeplearning.ai’s short courses so you can practice for free with local/open models. For the original, see the course pages.
