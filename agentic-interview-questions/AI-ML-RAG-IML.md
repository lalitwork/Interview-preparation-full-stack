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

### FDE Q6: What should an FDE do when customer stakeholders disagree about the problem or success criteria?

Identify who owns the workflow, who will use the solution, who approves risk, and who funds it. Interview affected groups, document the competing needs, and bring them together to agree on one prioritized use case, a baseline, and measurable acceptance criteria. If alignment is not possible, propose a small discovery or prototype that tests the disputed assumption before committing to a broad build.

**Practical example:** Support leadership wants faster replies while compliance wants fewer unsupported answers. Agree to measure both resolution time and policy-citation correctness in a limited pilot, rather than optimizing only for speed.

### FDE Q7: How should an FDE manage scope when a customer keeps adding requirements?

Keep a shared backlog and distinguish launch-critical requirements from later enhancements. For each new request, estimate its impact on value, risk, integration effort, and schedule; make the trade-off visible and get the accountable customer owner to approve changes to scope or timeline. Protect time for evaluation, security review, and operational readiness rather than treating them as optional polish.

**Practical example:** When a pilot expands from one document collection to six business units, pause to confirm permissions, data quality, and evaluation coverage before changing the delivery date or promising the broader rollout.

### FDE Q8: What should an FDE do when the customer's data is inaccessible, incomplete, or unreliable?

Confirm data ownership and authorization before access, then profile coverage, freshness, quality, and representativeness using approved samples. Explain how each gap affects the proposed outcome and agree on a remediation owner. Use synthetic or de-identified data for early interface work when appropriate, but do not present results from it as proof of production performance.

**Practical example:** If a policy index is missing recent revisions, show the customer which answers could be affected, pause claims about answer quality, and help establish an approved ingestion and update process before the pilot.

### FDE Q9: How can an FDE evaluate a solution when there are few labeled examples?

Start with domain experts to define expected outcomes and create a small, representative set of cases, including difficult, ambiguous, and unanswerable examples. Use expert review and explicit rubrics; expand the set from real pilot cases only with appropriate consent and data controls. Report uncertainty and sample limitations, and avoid treating model-generated labels or a small convenience sample as independent ground truth.

**Practical example:** For a low-volume claims workflow, have two authorized reviewers independently score a sample of redacted cases, resolve disagreements, and use the resulting rubric to evaluate a narrow pilot before scaling.

### FDE Q10: How should an FDE handle customer security, privacy, or compliance requirements that block a proposed integration?

Treat the requirements as design constraints, not obstacles to bypass. Involve the customer's security, privacy, legal, and platform owners early; document data flows, model providers, retention, access controls, and subprocessors; and offer compliant alternatives such as customer-controlled deployment, reduced data, or a narrower use case. Do not copy data to personal accounts, disable controls, or make compliance claims outside your authority.

**Practical example:** If external model processing is not approved, test the workflow with synthetic data while the customer evaluates an approved private endpoint; do not send real records to a public service to keep a demo on schedule.

### FDE Q11: How should an FDE choose an architecture under customer infrastructure constraints?

First establish the customer's supported runtime, identity, network, storage, deployment, and observability standards. Prefer the smallest design that fits those constraints and can be operated by the customer's team. Make dependencies, failure modes, upgrade paths, and ownership explicit; if a required capability is unavailable, negotiate a reduced scope rather than introducing an unsupported system silently.

**Practical example:** In a restricted network, use the customer's approved model endpoint and existing search service instead of adding a new hosted vector database that the platform team cannot reach or support.

### FDE Q12: What should a pilot's go/no-go decision include?

Agree on decision criteria before the pilot: target users and workflow, comparison baseline, minimum quality and safety thresholds, operational cost, adoption signals, and stop conditions. Review failures and subgroup or workflow differences, not just averages. Decide whether to expand, iterate, or stop; include rollback and a named decision owner so a pilot does not become an unreviewed permanent deployment.

**Practical example:** Expand a support assistant only if it improves handling time without lowering citation correctness, passes access-control tests, and has an acceptable human-review burden; otherwise keep it in draft-only mode or roll it back.

### FDE Q13: How should an FDE respond when users do not trust or adopt the delivered solution?

Observe the actual workflow and ask users where the solution creates friction or risk. Check whether the output is useful, explainable, timely, and integrated into existing tools; review rejection and edit patterns with users rather than pressuring them to accept suggestions. Address training or workflow gaps, and be willing to revise or stop the feature if it does not help.

**Practical example:** If support agents copy answers into a separate system because the pilot lacks links to source policies, prioritize that workflow integration and measure whether it reduces effort before changing the model.

### FDE Q14: What should an FDE do when a production issue affects a customer?

Follow the agreed incident process: acknowledge the report, assess scope and impact, preserve relevant logs under the customer's data policies, and involve the named technical and business owners. Mitigate safely—such as disabling a risky capability or returning to the prior workflow—then communicate verified facts and updates without speculation. After recovery, document root cause, corrective actions, and how the fix will be tested.

**Practical example:** If an update causes answers to cite outdated policies, switch the affected feature to human-reviewed drafts, identify which requests may have been impacted, notify the customer owner, and validate the index refresh before re-enabling automatic responses.

### FDE Q15: How should an FDE handle pressure to promise accuracy, savings, or a delivery date that has not been validated?

Separate demonstrated results from hypotheses and estimates. State the conditions, sample size, uncertainty, and operational assumptions behind any projection; propose a measurable test when evidence is missing. Escalate contractual, regulatory, or product commitments to the accountable owners rather than making guarantees on behalf of the organization.

**Practical example:** Instead of promising a 50% reduction in handling time after a short demo, agree to measure the current baseline and compare it with a controlled pilot that includes review and exception time.

### FDE Q16: What should an FDE include in a handoff when an engagement ends?

Transfer ownership, not just code. Provide the customer team with the architecture and data-flow diagrams, deployment and rollback steps, configuration and dependency inventory, operational dashboards, known limitations, evaluation results, incident contacts, and a prioritized backlog. Walk through the material with the receiving operators and confirm they can perform routine tasks without relying on undocumented knowledge.

**Practical example:** Before leaving a deployment, have the customer's on-call engineer rehearse a model-endpoint rollback and a document-index refresh in a staging environment.

### FDE Q17: How should an FDE prioritize work across multiple customer engagements?

Prioritize using customer impact, safety or contractual urgency, delivery commitments, dependencies, and the cost of delay. Make capacity and trade-offs visible to engagement owners, reserve time for production support, and avoid silently allowing the loudest request to displace critical work. Escalate conflicts that require a business decision rather than overcommitting and lowering quality everywhere.

**Practical example:** A production access-control issue affecting live users takes precedence over a new demo feature; notify the other customer, reset the milestone transparently, and agree on a revised plan.

---

[⬅ Return to Top](#ai-ml-rag-and-iml-unique-supplemental-questions) | [⬅ Return to Root README](../README.md)
