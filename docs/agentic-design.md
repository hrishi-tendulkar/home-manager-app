# Agentic Design Model

This document describes the agentic design model Home Manager is evolving toward. It outlines how AI responsibilities are decomposed and orchestrated as the product grows, even if the current implementation begins as a simpler, sequential pipeline.

The goal is to make AI behavior understandable, controllable, and aligned with product needs over time.

---

## Why an agentic model

Home-related workflows involve distinct types of reasoning:
- Interpreting messy, real-world inputs
- Mapping information into a stable structure
- Identifying follow-ups and open loops
- Providing guidance based on history and timing

An agentic model allows these responsibilities to be separated, reasoned about independently, and improved incrementally.

---

## Orchestrator

The orchestrator is responsible for:
- Receiving user inputs
- Assembling relevant context from the home record
- Selecting which workflows to run
- Coordinating specialist agents
- Returning a coherent response to the user

The orchestrator owns control flow rather than domain logic.

---

## Specialist agents

### Intake Agent

The Intake Agent focuses on understanding incoming information.

It extracts relevant facts from text, photos, or documents and identifies when clarification is needed. Its output is a normalized representation of what the user is trying to capture.

---

### Normalization Agent

The Normalization Agent maps interpreted inputs into the core data model.

It resolves naming variance, associates inputs with categories and services, and creates or updates occurrences as needed. This agent ensures consistency over time.

---

### Open Loops Agent

The Open Loops Agent identifies follow-ups implied by captured information.

This includes tasks such as scheduling a future service, tracking a pending action, or reminding the user at an appropriate time.

---

### Home Insights Agent

The Home Insights Agent operates over assembled context to provide summaries, guidance, and suggestions.

It focuses on helping users understand what has happened and what may need attention next.

---

## Context and memory

Agents operate over a shared context derived from the home record.

Context includes:
- Historical services and occurrences
- Recency and timing signals
- Relevant notes and attachments
- The user’s current intent

This shared context allows agents to behave consistently across interactions.

---

## Execution model

The agentic model does not require all agents to run on every interaction.

Execution may begin as a sequential pipeline and evolve toward more dynamic orchestration as complexity increases.

This allows the system to remain simple while preserving a clear path to richer behavior.

---

## Design intent

The agentic design emphasizes:
- Clear ownership of responsibilities
- Predictable behavior over time
- Incremental evolution rather than upfront complexity

The model supports modern AI capabilities while keeping the product grounded in real user needs and constraints.
