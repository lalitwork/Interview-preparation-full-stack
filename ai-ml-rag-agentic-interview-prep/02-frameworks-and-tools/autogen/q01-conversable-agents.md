[⬅ Back](../README.md)

# Q1. Conversable Agents

**Category:** Frameworks & Tools → AutoGen  
**Difficulty:** Intermediate  
**Tags:** autogen, conversable-agent, multi-agent, conversation

## Question

What are "conversable agents" in Microsoft AutoGen, and how do they enable multi-agent collaboration?

## Answer

**Conversable agents** are the core abstraction in AutoGen. They are agents that can send and receive messages, execute code, and interact with other agents or humans through a chat-based interface.

### Types of Conversable Agents

| Agent Type | Role |
|------------|------|
| `AssistantAgent` | LLM-driven agent that reasons and suggests tool calls or actions |
| `UserProxyAgent` | Represents the human; can execute code and seek user approval |
| `GroupChat` | Manages a group of agents speaking in turn |
| `Swarm` | Handoff-based multi-agent collaboration (lightweight) |

### Typical Multi-Agent Pattern

A coding task might use two agents:

1. **AssistantAgent (Coder):** Writes code and suggests fixes
2. **UserProxyAgent (Executor):** Runs the code in a sandbox, returns output, asks user for approval on sensitive operations

```
UserProxy → "Fix the bug in login.py"
    ↓
AssistantAgent → Analyzes code, suggests fix
    ↓
UserProxy → Applies fix, runs tests, reports results
    ↓
(Iterate until tests pass or user approves)
```

## Key Takeaways

- Conversable agents communicate via messages, not direct function calls
- `UserProxyAgent` bridges the gap between LLM suggestions and real-world execution
- AutoGen supports both two-agent and group-chat patterns

## Related Questions

- [AI guide: Multi-agent system design](../../AI-ML-RAG-IML.md#q68-how-should-multi-agent-systems-be-designed)

## References

- [AutoGen Documentation](https://microsoft.github.io/autogen/)

---

[⬅ Return to Root README](../../../README.md)