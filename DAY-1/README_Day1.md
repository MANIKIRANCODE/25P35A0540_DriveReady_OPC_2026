# Day 1: LLM Foundations, Prompt Engineering & Guardrails

## Overview
Day 1 introduces the fundamentals of connecting to Large Language Models (LLMs) using **LangChain** and **Groq**, crafting structured system prompts for domain-specific assistants, and applying safety guardrails against prompt injection.

---

## Key Concepts Covered

### 1. Environment & LLM Setup
* **Library Installation**: Installing `langchain_groq` to interface with Groq's high-speed inference engine.
* **API Authentication**: Securely loading `GROQ_API_KEY` from Google Colab Secrets (`google.colab.userdata`).
* **Model Initialization**: Instantiating `ChatGroq` using `openai/gpt-oss-120b` with `temperature=0` for deterministic, factual responses.

### 2. System Prompt Design
* Defined a clear persona and operational boundaries for **Sweet Crumbs Home Bakery**:
  * **Role**: Assistant for Sweet Crumbs Home Bakery.
  * **Facts**: Baked to order, 24-hour advance notice required, eggless versions available for all cakes.
  * **Rules**: Never promise delivery times; admit uncertainty when information is unknown.
  * **Format**: Polite tone, strictly under 60 words.

### 3. Prompt Guard & Safety
* Demonstrated adversarial prompt detection using the native `groq` SDK and the `meta-llama/llama-prompt-guard-2-22m` model.
* Evaluated jailbreak/override attempts (e.g., *"Ignore your previous instructions..."*), returning a high risk score (`~0.9989`) to flag unsafe inputs before reaching the primary assistant.

---

## Code Structure
1. **Setup**: Install `langchain_groq` and configure `GROQ_API_KEY`.
2. **Assistant Function (`ask`)**: Wraps `llm.invoke()` with `("system", SYSTEM)` and `("human", question)` tuples.
3. **Safety Check**: Uses `Groq().chat.completions.create()` with `llama-prompt-guard-2-22m` to score prompt injection risk.
