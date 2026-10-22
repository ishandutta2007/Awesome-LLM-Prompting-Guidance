# Awesome LLM Prompting & Guidance

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ishandutta2007/Awesome-LLM-Prompting-Guidance/pulls)

> A curated list of awesome **LLM prompting & guidance frameworks**, **structured output engines**, **constrained generation libraries**, and **prompt engineering tools** for production AI applications.

---

## Overview

Modern AI development has moved beyond brittle string templates and unpredictable markdown responses. **LLM Prompting & Guidance** tools empower developers to reliably control how Large Language Models generate text—enforcing strict JSON schemas, constraining token-level logits via grammars/regex, validating responses, and composing multi-step reasoning chains into deterministic, type-safe workflows.

Whether you are targeting hosted cloud APIs (OpenAI, Anthropic, Google Gemini) or running high-throughput self-hosted open-weight models (via vLLM, Ollama, TGI, or llama.cpp), this curated directory highlights the leading open-source libraries and SaaS solutions.

### Key Capabilities Covered
- **Structured Outputs & Schema Extraction**: Enforce Pydantic models, JSON Schemas, and TypeScript interfaces with automatic retry and validation.
- **Constrained Decoding & Token Masking**: Guide token logits with finite state machines (FSM) or context-free grammars (CFG) for 100% schema compliance.
- **Interleaved Generation & Prompt Control Flow**: Combine prompt logic, branching, loops, and generation in unified programs.
- **Guardrails & Evaluation**: Enforce safety rails, PII detection, toxicity filtering, and automated regression testing.

---

## Table of Contents

- [Quick Comparison Matrix](#quick-comparison-matrix)
- [SaaS & Hosted Platforms](#saas--hosted-platforms)
- [Open-Source Prompt Guidance Frameworks](#open-source-prompt-guidance-frameworks)
- [Prompt Engineering & Evaluation Tools](#prompt-engineering--evaluation-tools)
- [How to Choose the Right Tool](#how-to-choose-the-right-tool)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

---

## Quick Comparison Matrix

| Project | Approach | Best For | Backend Compatibility | Language / Ecosystem |
| :--- | :--- | :--- | :--- | :--- |
| **[Instructor](https://github.com/instructor-ai/instructor)** | Pydantic Schema Validation & Retry | Document extraction, function calling | OpenAI, Anthropic, Gemini, Mistral, Ollama | Python, TypeScript, Go |
| **[Outlines](https://github.com/dottxt-ai/outlines)** | Token-level Constrained Decoding (FSM/CFG) | Guaranteed 100% schema/JSON adherence | vLLM, llama.cpp, Transformers, TGI | Python |
| **[Guidance](https://github.com/guidance-ai/guidance)** | Interleaved Generation & Grammars | Complex branching, classification, grammar control | Local models, Transformers, select APIs | Python |
| **[BAML](https://github.com/BoundaryML/baml)** | Type-safe DSL + Prompt Playground | Microservices, enterprise prompt architectures | Multi-provider (OpenAI, Anthropic, local) | DSL (Python, TS, Go clients) |
| **[TypeChat](https://github.com/microsoft/TypeChat)** | TypeScript Schema Validation & Repair | Type-safe natural language interfaces | Hosted APIs (OpenAI, Azure OpenAI) | TypeScript / JavaScript |
| **[Guardrails AI](https://github.com/guardrails-ai/guardrails)** | Post-generation Validation Rails | Safety policies, PII filtering, structural validation | Multi-provider | Python |
| **[LMQL](https://github.com/eth-sri/lmql)** | Declarative Constraint Queries | Algorithmic prompts & declarative constraints | Local models, OpenAI | Python / LMQL |
| **[Marvin](https://github.com/prefecthq/marvin)** | High-level Agentic & Data Framework | Fast prototyping, agent state & memory | Multi-provider | Python |

---

## SaaS & Hosted Platforms

| Product | Pricing / Model | Free Tier Limits | Key Highlights |
| :--- | :--- | :--- | :--- |
| **[OpenAI Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)** | Pay-per-token API pricing (model dependent: e.g. GPT-4o, GPT-4o-mini) | No dedicated free tier; standard new account credits (when applicable) subject to expiration | Native server-side schema adherence guaranteeing 100% compliant JSON responses matching supplied JSON Schema without client-side parsing overhead. |

> [!NOTE]
> Most dedicated prompt guidance and constrained generation frameworks are open-source client/engine libraries rather than stand-alone SaaS products. Major cloud model providers offer proprietary schema compliance natively, but they do not serve as portable, cross-provider guidance frameworks.

---

## Open-Source Prompt Guidance Frameworks

### Category Leaders

- **[Instructor](https://github.com/instructor-ai/instructor)**  
  **The Pydantic-first structured extraction standard.**  
  With millions of monthly downloads, Instructor is the go-to solution for structured outputs across hosted LLM providers. By wrapping standard client SDKs with Pydantic models (`client.chat.completions.create(response_model=YourModel)`), it handles schema generation, validation, and automated retries when validation fails.  
  *Keywords*: `pydantic`, `structured-outputs`, `json-mode`, `data-extraction`

- **[Outlines](https://github.com/dottxt-ai/outlines)**  
  **The constrained decoding engine for guaranteed compliance.**  
  Outlines guides language model token sampling directly using regular expressions, JSON schemas, and context-free grammars (CFGs). It mathematically guarantees valid outputs by masking invalid tokens at inference time. Natively integrated with **vLLM**, it is the industry benchmark for high-throughput self-hosted inference.  
  *Keywords*: `constrained-decoding`, `vllm`, `regex-guided`, `cfgs`, `self-hosted`

- **[Guidance](https://github.com/guidance-ai/guidance)**  
  **The interleaved generation paradigm from Microsoft Research.**  
  Guidance lets developers interleave prompting, deterministic templating, logic, and generation into a unified execution flow. It eliminates parse errors by restricting output tokens to predefined choices, regex patterns, or grammars, while allowing conditional branching based on generated text.  
  *Keywords*: `token-healing`, `constrained-generation`, `grammar-based`, `prompt-flow`

- **[BAML](https://github.com/BoundaryML/baml)**  
  **The type-safe prompt DSL with dedicated VS Code playground.**  
  Boundary's domain-specific language treats LLM prompts as typed, testable software functions. Features an integrated VS Code preview playground with hot-reloading and generates fully typed clients for Python, TypeScript, and Go with first-class streaming support.  
  *Keywords*: `dsl`, `type-safety`, `developer-tools`, `prompt-testing`

- **[TypeChat](https://github.com/microsoft/TypeChat)**  
  **Microsoft's type-driven natural language interface.**  
  Uses TypeScript type definitions directly as the prompt contract. TypeChat prompts models, validates their response against the TypeScript compiler, and automatically repairs malformed outputs through conversational feedback.  
  *Keywords*: `typescript`, `type-safety`, `natural-language-interface`, `schema-repair`

- **[Guardrails AI](https://github.com/guardrails-ai/guardrails)**  
  **The comprehensive validation rails framework.**  
  Provides modular guardrails to verify structural integrity, PII exposure, hallucinations, and toxic content. Validators can be assembled into composite input/output guards with configurable policies (fix, filter, re-ask, or raise).  
  *Keywords*: `guardrails`, `ai-safety`, `validation`, `pii-redaction`

- **[LMQL](https://github.com/eth-sri/lmql)**  
  **The declarative query language for language models.**  
  Combines declarative SQL-like constraint specifications with Python control flow, enabling expressive token masking, multi-variable constraints, and optimized generation execution graphs.  
  *Keywords*: `query-language`, `declarative-prompting`, `token-constraints`

- **[Marvin](https://github.com/prefecthq/marvin)**  
  **Batteries-included agentic and data framework by Prefect.**  
  A lightweight abstraction for extracting structured entities, categorizing text, and building autonomous multi-agent pipelines with built-in memory and state management.  
  *Keywords*: `agents`, `prefect`, `synthetic-data`, `structured-text`

- **[Jsonformer](https://github.com/1rgs/jsonformer)**  
  **Bulletproof JSON generation for Hugging Face Transformers.**  
  Generates fixed JSON structure tokens deterministically and queries the model only for dynamic value fields, accelerating decoding while ensuring syntactic validity.  
  *Keywords*: `huggingface`, `jsonformer`, `json-decoding`

---

## Prompt Engineering & Evaluation Tools

- **[LM Format Enforcer](https://github.com/noamgat/lm-format-enforcer)** — High-performance token filtering library for JSON Schemas and regex on top of vLLM, Transformers, and llama.cpp.
- **[DSPy](https://github.com/stanfordnlp/dspy)** — Stanford's framework for programmatically optimizing prompt instructions and few-shot examples through automated metric compilation.
- **[Promptfoo](https://github.com/promptfoo/promptfoo)** — CLI and CI/CD testing framework for LLM security red-teaming, prompt regression evaluation, and benchmark grading.

---

## How to Choose the Right Tool

| Use Case | Recommended Solution |
| :--- | :--- |
| **Calling hosted APIs (OpenAI, Anthropic, Gemini)** | Use **[Instructor](https://github.com/instructor-ai/instructor)** for clean Pydantic integration or **[BAML](https://github.com/BoundaryML/baml)** for multi-language typed interfaces. |
| **Self-hosting open-weight models (vLLM / llama.cpp)** | Use **[Outlines](https://github.com/dottxt-ai/outlines)** for guaranteed 100% token-level schema adherence without retries. |
| **Interleaved prompt logic & branching grammars** | Use **[Guidance](https://github.com/guidance-ai/guidance)** to build stateful generation programs. |
| **TypeScript / Fullstack Web applications** | Use **[TypeChat](https://github.com/microsoft/TypeChat)** or **[Instructor TS](https://github.com/instructor-ai/instructor-js)**. |
| **Safety, PII, and content moderation** | Use **[Guardrails AI](https://github.com/guardrails-ai/guardrails)** alongside your generation pipeline. |
| **Prompt optimization & automated tuning** | Use **[DSPy](https://github.com/stanfordnlp/dspy)** to compile prompts algorithmically. |

---

## How to Contribute

Contributions are welcome! Please follow these simple guidelines:

1. Fork the repository.
2. Add or update tools following the established format:
   - Name, official link, crisp summary, and key differentiating technical capabilities.
   - For SaaS products, include pricing model and free tier specifics.
3. Submit a pull request with a descriptive title and summary.

---

## Disclaimer

- This is a community-curated collection intended for educational and engineering reference.
- **Validation vs. Constrained Decoding**: Post-generation validators (e.g. Instructor, Guardrails) retry upon parse failures; token-level decoders (e.g. Outlines, Guidance) constrain generation directly at inference time. Select the tool tailored to your deployment model.

---

**Maintained by the open-source AI engineering community.**
