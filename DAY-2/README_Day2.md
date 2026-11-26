# Day 2: OpenAI-Compatible APIs, Python Data Structures & Stateful Chat Loops

## Overview
Day 2 transitions to using the **OpenAI Python SDK** pointed at Groq's OpenAI-compatible endpoint, builds core Python foundations (dictionaries, JSON, functions, decorators, error handling), and implements a multi-turn conversational loop with sliding-window memory.

---

## Key Concepts Covered

### 1. OpenAI SDK with Groq Endpoint
* Configured `OpenAI(api_key=..., base_url="https://api.groq.com/openai/v1")` to interact with `openai/gpt-oss-120b`.
* Inspected token usage metrics (`prompt_tokens`, `completion_tokens`, `reasoning_tokens`, `total_tokens`) via `response.usage`.
* Added multilingual support (English and Telugu) and fallback instructions (*"I'll check with the owner."*).

### 2. Python Essentials for AI Applications
* **Dictionaries & Safe Lookups**: Storing menu prices (`MENU`) and using `.get()` to avoid `KeyError` crashes on unavailable items.
* **JSON Serialization**: Converting Python order dictionaries to JSON strings and back using `json.dumps()` and `json.loads()`.
* **Functions & Decorators**: Writing typed helper functions (`get_price`) and wrapping them with a custom `@log_call` decorator using `functools.wraps` to trace inputs and outputs.
* **Exception Handling**: Using `try/except` blocks to gracefully catch `NameError`, `RateLimitError`, and `APIConnectionError`.

### 3. Stateful Conversational Chatbot
* Built an interactive `while True` CLI chat loop (`chat(user_text)`).
* Maintained conversation context in a `history` list while capping context length with a sliding window (`MAX_TURNS = 8`) to manage token usage.

---

## Code Structure
1. **Client Configuration**: Initialize `OpenAI` client with Groq base URL.
2. **Menu & Order Utilities**: `MENU` dict, JSON conversions, and `@log_call` decorated `get_price()`.
3. **Interactive Chat Loop**: `chat()` function managing `history`, sliding window truncation, and API error handling.
