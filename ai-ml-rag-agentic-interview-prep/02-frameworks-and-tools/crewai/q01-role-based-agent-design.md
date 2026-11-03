[⬅ Back](../README.md)

# Q1. Role-Based Agent Design

**Category:** Frameworks & Tools → CrewAI  
**Difficulty:** Intermediate  
**Tags:** crewai, roles, agents, tasks, multi-agent

## Question

How does CrewAI's role-based agent design work, and what are the key abstractions (agents, tasks, crews, processes)?

## Answer

**CrewAI** organizes agents around roles, similar to a human team. Each agent has a defined role, goal, and backstory, and works on tasks within a crew.

### Key Abstractions

| Abstraction | Purpose |
|-------------|---------|
| **Agent** | A team member with a role (e.g., "Researcher", "Writer", "Reviewer") |
| **Task** | A specific assignment with a description and expected output |
| **Crew** | A team of agents working together on related tasks |
| **Process** | The orchestration strategy (sequential or hierarchical) |

### Role-Based Example

```
Crew: Content Creation Pipeline
├── Agent: Researcher (role: gather facts and sources)
│   └── Task: Research the topic and compile key findings
├── Agent: Writer (role: draft engaging content)
│   └── Task: Write an article based on research
└── Agent: Reviewer (role: edit for quality and accuracy)
    └── Task: Review and refine the article
```

### Process Types

- **Sequential:** Tasks execute one after another (output of task N feeds task N+1)
- **Hierarchical:** A manager agent coordinates and delegates tasks to worker agents

## Key Takeaways

- Roles give agents context and purpose, improving output relevance
- Tasks define what success looks like for each step
- Processes determine how agents coordinate (sequential vs. hierarchical)

## Related Questions

- [Agent Architecture: Q1. Single-Agent Architecture](../../01-agent-architecture/q01-single-agent-architecture.md)

## References

- [CrewAI Documentation](https://docs.crewai.com/)

---

[⬅ Return to Root README](../../../README.md)