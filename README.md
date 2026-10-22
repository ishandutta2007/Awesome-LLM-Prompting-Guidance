# Awesome-LLM-Prompting-Guidance

# Top LLM Prompting & Guidance Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Structured Output, Constrained Generation & Self-Hosted Prompt Control*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **LLM Prompting & Guidance**. These tools give developers control over how language models generate text—enforcing schemas, constraining token-level outputs, validating responses, and composing multi-step prompts—moving beyond brittle string templates toward reliable, type-safe LLM interactions.

**Examples** include Instructor, Outlines, Guidance, BAML, LMQL, Jsonformer, TypeChat, Guardrails AI, and Marvin (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, model-agnostic generation control, and transparent prompt execution—ideal for teams building production LLM applications without vendor lock-in or per-token guidance fees. The open-source landscape is anchored by **Instructor** (the Pydantic-first extraction standard), **Outlines** (the constrained decoding engine for JSON schemas and grammars), **Guidance** (the interleaved generation/programming paradigm), and **BAML** (the type-safe DSL with VS Code playground), with **Guardrails AI** providing validation rails and **Marvin** offering a batteries-included agent framework.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[OpenAI Structured Outputs](https://openai.com/)**  
  OpenAI's native API feature for enforcing JSON Schema adherence on model responses. Available with GPT-4o and newer models. Server-side enforcement means no client-side parsing logic required. Proprietary, API-only—included here as the baseline against which open-source guidance tools are measured.

- **No other dedicated SaaS platforms exist for prompt guidance.** Most tools in this category are open-source libraries that run in your application process. Cloud LLM providers offer structured output features natively, but these are model-specific and not portable guidance frameworks.

## Open-Source GitHub Projects

- **[Instructor](https://github.com/instructor-ai/instructor)**  
  **The Pydantic-first extraction standard.** The most widely adopted library for getting structured outputs from LLMs, with 3M+ monthly downloads. **How it works**: define a Pydantic model, pass it to `client.chat.completions.create(response_model=YourModel)`, and Instructor handles schema generation, validation, and retry on failure. **Strengths**: works across OpenAI, Anthropic, Google, Mistral, Cohere, Ollama, and more; integrates seamlessly with existing LLM client code; excellent for document extraction and data parsing . Best for Python developers who want minimal friction when extracting typed data from LLM responses.

- **[Outlines](https://github.com/dottxt-ai/outlines)**  
  **The constrained decoding engine.** Guides model token logits using regular expressions, JSON schemas, and context-free grammars (CFGs) to **guarantee 100% compliant output**—not just validate after the fact . **Key strength**: integrates with vLLM for high-throughput self-hosted inference, making it the go-to choice for teams running open-weight models . **Trade-offs**: requires control over the inference backend; not all hosted APIs expose the token-level access Outlines needs. Best for teams self-hosting models (via vLLM, TGI, or llama.cpp) that need guaranteed schema compliance.

- **[Guidance](https://github.com/guidance-ai/guidance)**  
  **The interleaved generation paradigm.** Microsoft Research's prompting language that lets you interleave prompts, generation, and logical control into a single continuous flow matching how the model processes text . **Key capability**: constrain generation to specific choices, regex patterns, or context-free grammars while maintaining the ability to branch and loop based on model output . **Trade-offs**: introduces new concepts (grammar construction, generation state, backend compatibility) and requires model providers that expose token-level control . Best for applications requiring controlled generation workflows—classification systems, structured reasoning, and outputs that combine generated text with deterministic logic.

- **[BAML](https://github.com/BoundaryML/baml)**  
  **The type-safe DSL with VS Code playground.** Boundary's domain-specific language for defining LLM functions with typed inputs and outputs. **Developer experience**: VSCode extension with a **playground for testing prompts without leaving the editor**, hot-reloading, and full visibility into the rendered prompt and raw cURL request . **Type safety**: generates Python/TypeScript/Go clients with fully typed outputs, even for streaming structured data . **Trade-offs**: introduces a new language and build step; teams must adopt BAML's tooling and maintain generated clients . Best for teams with many LLM-powered functions who want explicit interfaces between AI components and application code.

- **[LMQL](https://github.com/eth-sri/lmql)**  
  **The query language for LLMs.** A programming language that extends Python with SQL-like constraints for LLM generation. **Strengths**: declarative constraints on output structure; supports complex control flow within prompts. **Trade-offs**: smaller community than Instructor or Outlines; requires learning LMQL syntax. Best for developers who prefer declarative constraint specification over imperative prompt construction.

- **[Jsonformer](https://github.com/1rgs/jsonformer)**  
  **The bulletproof JSON generator.** Wraps Hugging Face models and fills in fixed JSON tokens during generation, delegating only content tokens to the model . **Key insight**: in structured data, many tokens are predictable—only the actual values need generation. **Trade-offs**: limited to Hugging Face transformers integration; supports a subset of JSON Schema (number, boolean, string, array, object); less actively maintained than alternatives. Best for Hugging Face users who want guaranteed JSON correctness with minimal infrastructure changes.

- **[TypeChat](https://github.com/microsoft/TypeChat)**  
  **Microsoft's type-driven natural language interface.** Uses TypeScript types as the specification for LLM responses—define your domain types, and TypeChat constructs the prompt, validates the response against those types using the TypeScript compiler, and **repairs non-conforming output** through iterative LLM interaction . **Key benefit**: safety through validation before taking action; the model's output must conform to your types or be repaired . **Trade-offs**: currently TypeScript/JavaScript only; best suited for applications adding natural language interfaces to existing typed codebases. Best for TypeScript projects that want to translate user intent into validated, typed actions.

- **[Guardrails AI](https://github.com/guardrails-ai/guardrails)**  
  **The validation rails framework.** Applies quality controls to LLM outputs through **validators**—methods that encode criteria, check values, and apply on-fail policies (reask, fix, filter, exception) . **Validators** are published as pip packages (`guardrails-ai-toxic-language`, `guardrails-ai-detect-pii`, etc.) and can be combined into input/output guards . **Trade-offs**: validation happens after generation (unlike Outlines' constrained decoding); requires installing and configuring individual validators. Best for teams that need post-generation safety checks—PII detection, toxicity filtering, provenance verification—alongside structured output enforcement.

- **[Marvin](https://github.com/prefecthq/marvin)**  
  **The batteries-included agent framework.** Prefect's Python framework for building AI applications with smart defaults for state management, conversation history, and multi-agent coordination . **Key features**: `marvin.run()` for one-line tasks; `marvin.Agent` for specialized personas; `result_type` parameter for structured Pydantic outputs; persistent `Memory` modules across conversations . **Trade-offs**: more of an application framework than a pure guidance tool; less focused on token-level generation control. Best for developers who want a higher-level abstraction for building agents and workflows without assembling every piece manually.

### Additional Strong Open-Source Options

- **LM Format Enforcer** — Token filtering for JSON schema compliance, focused on integration with compatible inference pipelines. Best for teams already using its supported inference engines .
- **DSPy** — Stanford's declarative framework that compiles and optimizes prompts programmatically. Best for teams that want to move beyond hand-crafted prompts toward algorithmic optimization .
- **Promptfoo** — CLI for test-driven prompt engineering and LLM red-teaming. Best for CI/CD-integrated prompt regression testing .
- **Frameworks for building custom systems**: Use **Instructor** for Pydantic-based extraction on hosted APIs. Use **Outlines** with **vLLM** for guaranteed schema compliance on self-hosted models. Use **Guidance** when you need interleaved generation and logic. Use **BAML** when you want a type-safe DSL with a dedicated playground. Pair **Guardrails AI** for post-generation validation. Use **Marvin** as a higher-level agent framework when you want less assembly.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Validation vs. constrained decoding is the key distinction**: Instructor and Guardrails validate after generation and retry on failure; Outlines and Guidance constrain token generation to prevent invalid output in the first place . The right choice depends on whether you control the inference backend.
- **Not all tools work with all providers**: Outlines requires token-level access typically available only with self-hosted models or specific inference engines. Instructor and Marvin work across hosted APIs. Verify provider compatibility before committing .
- **BAML introduces a new language and build step**: evaluate whether your team wants to adopt its tooling versus using a Python-native library like Instructor .

---

**Made for AI engineers, prompt engineers, and developers building reliable LLM applications.**  
Let's make LLM prompting and guidance more open, type-safe, and controllable.
