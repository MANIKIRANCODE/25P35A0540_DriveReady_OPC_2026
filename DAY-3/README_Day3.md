# Day 3: LangChain Expression Language (LCEL), Evaluation & Agent Basics

## Overview
Day 3 modernizes the assistant using **LangChain Expression Language (LCEL)** chains, structured message history placeholders, automated CSV-based evaluation testing, and an introduction to LangChain agents.

---

## Key Concepts Covered

### 1. LCEL Chains & Conversation Memory
* Built a modular pipeline using the pipe operator:
  ```python
  chain = prompt | llm | StrOutputParser()
  ```
* Used `ChatPromptTemplate.from_messages()` paired with `MessagesPlaceholder("history")` to dynamically inject prior user and AI turns into every prompt.
* Updated the `ask(question)` helper to append `("human", question)` and `("ai", answer)` tuples to `history`.

### 2. Automated Prompt Evaluation (`run_tests`)
* Created a test runner using Python's `csv.DictReader` to evaluate model responses against `/content/test.csv`.
* Checked whether expected keywords (`must_include`) appeared in the model's output across test cases (pricing, eggless options, same-day delivery constraints, out-of-area delivery, and bulk math).
* Calculated and reported overall pass rates (e.g., `3/5 passed (60%)`) to identify prompt edge cases.

### 3. Introduction to LangChain Agents
* Initialized a foundational agent using `create_agent(model=llm, tools=[], system_prompt=SYSTEM)` from `langchain.agents`, preparing the architecture for tool calling in subsequent sessions.

---

## Code Structure
1. **LCEL Pipeline**: `ChatPromptTemplate` + `MessagesPlaceholder` + `ChatGroq` + `StrOutputParser`.
2. **Memory Helper (`ask`)**: Invokes the chain and updates the `history` list.
3. **Evaluation Suite (`run_tests`)**: Reads test cases from CSV and scores response accuracy.
4. **Agent Setup**: Basic agent instantiation with `create_agent` (ready for custom tools).
