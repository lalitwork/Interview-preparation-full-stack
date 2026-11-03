[⬅ Back](./README.md)

# Q1. Single-Agent Architecture

**Category:** Agent Architecture  
**Difficulty:** Beginner  
**Tags:** architecture, single-agent, perception, action, loop

## Question

Describe the architecture of a single AI agent. What are its core components and how do they interact?

## Answer

A single-agent architecture follows the classic **perception → reasoning → action → observation** loop.

### Core Components

```
┌─────────────────────────────────────┐
│              GOAL                   │
└──────────────┬──────────────────────┘
               ▼
┌─────────────────────────────────────┐
│         PLANNING MODULE             │
│  (decompose goal into sub-tasks)    │
└──────────────┬──────────────────────┘
               ▼
┌─────────────────────────────────────┐
│         REASONING (LLM)             │
│  (decide next action + args)        │
└──────────────┬──────────────────────┘
               ▼
┌─────────────────────────────────────┐
│         ACTION / TOOL USE           │
│  (call API, run code, search web)   │
└──────────────┬──────────────────────┘
               ▼
┌─────────────────────────────────────┐
│         OBSERVATION                 │
│  (receive result from environment)  │
└──────────────┬──────────────────────┘
               ▼
        MEMORY (short + long term)
```

### Component Descriptions

1. **Goal / Objective** — What the agent is trying to achieve
2. **Planning Module** — Breaks the goal into executable sub-tasks
3. **Reasoning (LLM)** — The "brain" that decides what to do next
4. **Action / Tool Use** — Executes decisions via tools, APIs, or code
5. **Observation** — Captures the outcome of each action
6. **Memory** — Stores conversation history, past actions, and learned context

### Example Flow

A coding agent tasked with "fix a bug in the login module":
1. **Plan:** Read code → Reproduce bug → Identify root cause → Fix → Test
2. **Reason:** "I need to first read the login controller file"
3. **Action:** Call `read_file("src/auth/login.py")`
4. **Observe:** File content returned, revealing a missing null check
5. **Adjust:** Call `edit_file()` to add the null check, then run tests

## Key Takeaways

- Single-agent architecture is a loop, not a linear pipeline
- The LLM is the reasoning engine; tools are the hands; memory is the context
- Each iteration produces new observations that inform the next action

## Related Questions

- [Core Concepts: What is an AI agent?](../AI-ML-RAG-IML.md#q14-what-are-ai-agents-and-how-are-they-different-from-a-single-model-call)
- [AI guide: Multi-agent system design](../AI-ML-RAG-IML.md#q68-how-should-multi-agent-systems-be-designed)

## References

- [LangGraph: Agent Architecture](https://langchain-ai.github.io/langgraph/)

---

[⬅ Return to Root README](../../README.md)