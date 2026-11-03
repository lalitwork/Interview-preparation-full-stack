[⬅ Back](../README.md)

# Q1. LangGraph State Machines

**Category:** Frameworks & Tools → LangChain  
**Difficulty:** Intermediate  
**Tags:** langgraph, langchain, state-machine, agents

## Question

How does LangGraph enable stateful, cyclic agent architectures, and what is the role of the graph state?

## Answer

**LangGraph** is a library built on LangChain for building stateful, multi-actor applications with LLMs. Unlike standard LangChain chains (which are DAGs), LangGraph supports **cycles** — essential for agentic loops where an agent may need to retry, reflect, or iterate.

### Core Concepts

1. **Graph State** — A shared, typed object (e.g., `TypedDict` or Pydantic model) that persists across all nodes in the graph. Nodes read and write to this state.

2. **Nodes** — Functions that take the current state, perform work (e.g., call an LLM, invoke a tool), and return state updates.

3. **Edges** — Define transitions between nodes. Can be:
   - **Direct edges** — Always go from node A to node B
   - **Conditional edges** — Router functions that decide the next node based on state

4. **Checkpoints** — LangGraph can persist state at each step, enabling time-travel debugging, human-in-the-loop interrupts, and long-running workflows.

### Example: ReAct Agent Graph

```
START → [Agent Node] → [Tools Node]
    ↖__________________↗
     (conditional loop)
```

1. **Agent Node:** Reasons about what to do next, emits tool calls or a final answer
2. **Tools Node:** Executes the requested tools, returns results to state
3. **Conditional Edge:** If the agent wants to call more tools, loop back to Tools Node; otherwise, proceed to END

## Key Takeaways

- LangGraph enables cyclic agentic loops (unlike DAG-based chains)
- Graph state is the single source of truth shared across nodes
- Checkpoints enable persistence, retries, and human-in-the-loop workflows

## Related Questions

- [Core Concepts index](../../00-core-concepts/README.md)
- [AI guide: The ReAct pattern](../../AI-ML-RAG-IML.md#q65-what-is-the-react-pattern)

## References

- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)

---

[⬅ Return to Root README](../../../README.md)