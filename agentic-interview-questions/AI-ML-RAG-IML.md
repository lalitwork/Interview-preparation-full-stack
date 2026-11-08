[⬅ Back](./README.md) | [⬅ Return to Root README](../README.md)

# AI, ML, RAG, and IML: Unique Supplemental Questions

The [comprehensive AI question bank](./AI-Question-Bank-Answered.md) is the canonical source for general AI, machine learning, RAG, and agentic interview topics. This guide keeps only the distinct questions about Forward Deployed Engineering (FDE) and customer integration, avoiding repeated questions from that bank.

Here, **IML** means intelligent machine-learning applications: systems that combine models with software, data, tools, and operational controls. The acronym is not universally standardized, so define it when you use it.

## Original Practice Prompts

1. Design an evaluation set for a policy assistant, including unanswerable questions.
2. Compare vector-only retrieval with BM25 plus vector search using a measurable test plan.
3. Describe a production failure and trace it to ingestion, retrieval, generation, or authorization.

## Forward Deployed Engineering

### FDE Q1: What is a Forward Deployed Engineer (FDE)?

An FDE works closely with a customer or operational team to understand a concrete problem, integrate with real systems, and deliver a useful production solution. The role combines engineering with discovery, rapid iteration, and deployment responsibility. Success is measured by durable customer outcomes, not by the number of demos or model calls.

**Practical example:** An FDE shadows support staff, observes repeated time spent searching policy pages, prototypes a cited search assistant in the customer's environment, and measures whether it reduces handling time without increasing policy errors.

### FDE Q2: How should an FDE discover the right AI problem?

Start by observing the user's workflow, identifying its costly or error-prone steps, and determining what decision or action would improve the outcome. Establish a baseline, constraints, data access, and acceptable error levels before selecting a model. Sometimes a rules engine, search improvement, or workflow automation is the better answer.

**Practical example:** If users repeatedly enter the same known values into a form, automate the deterministic field mapping; reserve an LLM for the genuinely ambiguous free-text classification step.

### FDE Q3: What does good FDE customer integration involve?

Map the customer's systems, identity model, data ownership, network constraints, and operational practices before choosing an integration. Build against supported APIs, minimize data movement, and make failures visible to the customer team. Document deployment, support ownership, and upgrade paths so the solution remains maintainable after the initial engagement.

**Practical example:** Before connecting a customer's document store, agree which folders are in scope, use their identity provider for user permissions, and deploy through their approved network path rather than copying all documents to an uncontrolled account.

### FDE Q4: How should FDE success be measured?

Agree on an operational metric such as reduced handling time, fewer missed cases, improved resolution quality, or lower manual effort. Establish a baseline and account for adoption, exception rates, and review cost. A technically successful deployment that users do not trust or adopt has not solved the customer problem.

**Practical example:** Compare median resolution time and policy-correction rate for a pilot group against a similar group using the old workflow, while also tracking how often agents accept or edit suggested answers.

### FDE Q5: How should an FDE handle a customer request that is not a good AI use case?

Explain the mismatch using the customer's goals, risk tolerance, and evidence, then propose a simpler option such as rules, search, or process redesign. Be clear about limitations instead of forcing a model into the solution. Trust is built by solving the actual problem, even when the answer is not generative AI.

**Practical example:** If a customer only needs invoices routed by a fixed vendor code, propose a deterministic rules-based workflow; reserve AI for the separate task of extracting inconsistent descriptions from scanned invoices.

---

[⬅ Return to Top](#ai-ml-rag-and-iml-unique-supplemental-questions) | [⬅ Return to Root README](../README.md)
