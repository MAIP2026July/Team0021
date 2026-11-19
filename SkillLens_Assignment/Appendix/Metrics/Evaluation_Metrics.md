# SkillLens: Evaluation Metrics

This appendix defines how scoring quality, confidence, reporting and export are measured, and the thresholds that must be met before a skill area is released to learners or partners.

---

## 1. AI Task Definition

SkillLens scores open-ended responses to realistic scenarios. For each objective, the language model assigns an ordinal score from 0 to 3 and returns a verbatim quotation from the response as evidence. The model selects from validated content: scenarios, objectives and level descriptors are authored and reviewed by people. The model does not define objectives or rubric levels, and it does not determine confidence.

---

## 2. Defined Terms

| Term | Definition | Measurement | Target |
|---|---|---|---|
| Objective score | Score from 0 to 3 for one objective in one attempt | Model output, validated against the rubric | Defined per objective |
| Scenario score | Average of the four objective scores in one attempt | Calculated | Defined |
| Latest scenario score | Scenario score from the learner's most recent attempt at that scenario | Calculated | Defined |
| Skill proficiency | Average of the latest scenario scores for the scenarios the learner has attempted in a skill area; unattempted scenarios are excluded | Calculated | Shown with "n of 3 scenarios attempted" |
| Improvement | Latest score minus first score, for the same scenario or skill area | Calculated | Reported |
| Agreement with expert consensus | Quadratic weighted kappa (QWK) between model scores and consensus scores, averaged across objectives | Reference set; consensus from two graders with adjudication | QWK ≥ 0.70 |
| Within-one-level agreement | Share of objective scores within one level of consensus | Reference set | ≥ 85% |
| Human reliability | QWK between the two graders before adjudication | Reference set | ≥ 0.70; if not met, the rubric is revised before the model is evaluated |
| Evidence verifiability | Share of displayed quotations found in the learner's response (case and whitespace normalised) | Automated check on every attempt | 100% |
| Run consistency | Share of objective scores identical across the three runs of an attempt | Automated, per skill area | ≥ 90% identical; none differing by two or more levels |
| Routing recall | Share of model errors of two or more levels that are routed to review | Reference set | ≥ 80% |
| Paired-style shift | Mean difference between a response and its paired rewrite in a different register or language style | Paired-style test set | ≤ 0.5 level |
| Group agreement gap | Difference in QWK between writing-style or language groups | Paired-style test set | ≤ 0.10 |
| Keyword-only score | Mean score for responses that list terms without reasoning | Keyword-only test set | ≤ 1 per objective |
| Report consistency | Share of report values that match the underlying attempt records | Automated reconciliation | 100% |
| Export completeness | Share of exported records containing every defined field | Automated check on each export | 100% |
| Export parity | Share of CSV and JSON exports whose values match | Automated comparison | 100% |
| Reviewer override rate | Share of reviewed results where at least one objective score is changed | Audit log | Reported per skill area |
| Reviewer turnaround | Time from a result entering the review queue to a reviewer decision | Audit log | Reported; target set in pilot |
| Follow-up improvement | Share of follow-up attempts where the objective score is higher than in the first attempt | Learner records | Reported per skill area |
| Scoring latency | Time from submission to displayed result | Monitoring | 95th percentile under 10 seconds |
| Report latency | Time to load a report for up to 5,000 learners | Monitoring | 95th percentile under 3 seconds |

---

## 3. Reference Set

- **Size:** 40 responses per live skill area, spread across its three scenarios (about 13 or 14 per scenario).
- **Coverage:** responses at weak, partial and strong quality for each objective.
- **Grading:** two graders score each response per objective without seeing model output. Disagreements of more than one level are adjudicated, and the reason is recorded.
- **Stress sets:** 12 paired-style responses (same content, different register or language) and 6 keyword-only responses per skill area.
- **Authorship:** the reference set is written and graded by the product team. This limits realism and is stated in the final report.

Total reference responses for the three live skill areas: 120, plus stress sets.

---

## 4. Scenarios and Rubrics

Each live skill area has three scenarios and four objectives. Each objective has level descriptors for 1, 2 and 3. A score of 0 means the objective is not addressed. A score above 0 requires a verbatim quotation.

### 4.1 Data Structures and Algorithms

**DSA-1: The High-Traffic Flash Sale** (heaps, top-K tracking)

You are engineering the backend for a flash sale with a live leaderboard of the top 10 best-selling items, updated as purchases arrive. Sorting after every purchase is too slow. Which data structure and algorithm maintain the top 10 efficiently, and what is the time complexity of an incoming purchase event?

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| O1 | Choose the data structure | Names a structure without a reason | Names a min-heap of size K or a hash map, with a reason | Uses a min-heap of size K with a hash map for counts, and rejects a full sort with a reason |
| O2 | Analyse time complexity | States a complexity without a reason | States O(log K) per heap update, with the reason | Gives the update cost, including the hash map lookup, and the cost of reading the top K |
| O3 | Analyse space complexity | Mentions memory | Contrasts O(N) for unique items with O(K) for the heap | Explains the memory trade-off and what bounds growth |
| O4 | Explain trade-offs and limits | States one limitation | Explains a limitation that affects results, such as ties or update order | Explains when the approach fails and what would change the design |

**DSA-2: Degrees of Separation** (graph traversal and shortest path)

A professional network needs the shortest connection path between two users, on a graph with hundreds of millions of nodes. Which traversal finds the shortest path in an unweighted graph, and how would you handle weighted connections?

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| O1 | Choose the algorithm | Names a graph traversal without a reason | Names breadth-first search for unweighted graphs, with a reason | Names breadth-first search for unweighted graphs and Dijkstra's algorithm or A* for weighted graphs, with reasons |
| O2 | Analyse time complexity | States a complexity | States O(V + E) for breadth-first search | Gives O(V + E), and explains the cost of the priority queue for weighted search |
| O3 | Storage and memory | Mentions the graph in memory | Represents the graph as adjacency lists | Adds a strategy for not loading the whole graph, such as lazy loading or distributed queries |
| O4 | Explain trade-offs and limits | States one limitation | Explains a limitation that affects results, such as weight definitions | Explains when the approach fails for very large or changing graphs |

**DSA-3: The Rate Limiter for API Protection** (sliding window, deque, memory bounds)

Each user may make at most 100 requests in any 60-second window. Storing every timestamp uses too much memory. Design the data structures and data flow for a sliding-window limiter with minimal latency.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| O1 | Choose the data structure | Names a structure without a reason | Names a deque of timestamps or time buckets, with a reason | Explains the deque or bucket design, and how it tracks the sliding window |
| O2 | Analyse time complexity | States a complexity | States O(1) amortised per check | Explains amortised O(1), including removal of expired entries |
| O3 | Analyse space complexity | Mentions memory | Bounds memory by the request limit per user | Bounds memory per user at O(K) with K ≤ 100, and explains the bucket trade-off |
| O4 | Explain trade-offs and limits | States one limitation | Explains a limitation, such as accuracy of bucket boundaries | Explains how expired entries are removed so memory does not grow, and what happens under bursts |

### 4.2 Communication

**COM-1: Project delay message.** A project will slip by two weeks because of a data-quality issue. Write the message to the finance director, with impact, reason and next steps.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| C1 | Structure the message | Has some order | Leads with the key point, then reason and next steps | Leads with the key point, states impact and reason, and ends with the next steps and owner |
| C2 | Adapt to the audience | Refers to the audience | Chooses detail that suits a finance reader | Explains what this audience needs and chooses detail to match |
| C3 | Handle questions and challenge | Anticipates a question | Acknowledges the concern and states a next step | Supports the answer with evidence or a timeline |
| C4 | Write concisely | Removes some detail | Keeps the key point in the first sentence | Removes detail without losing the key point, and explains what was kept |

**COM-2: Explaining a report format.** A new team member asks why the team uses a particular report format. Write the explanation, then answer the follow-up: why not change it?

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| C1 | Structure the message | Has some order | Explains the format in steps | Explains the format in steps, and the purpose of each part |
| C2 | Adapt to the audience | Refers to a new team member | Uses an example or plain language | Uses an example and explains why it fits a newcomer |
| C3 | Handle questions and challenge | Responds to the follow-up | Acknowledges the change question and states a reason | Gives a reason with evidence, and a condition under which the format would change |
| C4 | Write concisely | Removes some detail | Keeps the explanation short | Keeps the answer short without losing the reason |

**COM-3: Handling a challenge from a senior stakeholder.** During a review, a senior stakeholder challenges your recommendation. Write how you respond.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| C1 | Structure the message | Has some order | Answers first, then gives the reason | Answers first, gives the reason and evidence, then the options |
| C2 | Adapt to the audience | Refers to the stakeholder | Responds to what the stakeholder cares about | Names the stakeholder's priority and responds to it |
| C3 | Handle questions and challenge | Acknowledges the challenge | Clarifies and states a follow-up | Clarifies, supports the answer with evidence or options, and commits to a timeline |
| C4 | Write concisely | Removes some detail | Keeps the response short | Keeps the response short without losing the recommendation |

### 4.3 Generative AI

**GAI-1: Choosing an approach for a support assistant.** A company wants a support assistant that answers questions from its policy documents, which change monthly. Compare retrieval-augmented generation with fine-tuning, and recommend one with reasons.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| G1 | Frame the problem | Restates the request | Identifies that the documents change and must be current | Identifies the change frequency, the need for citations, and the cost of updates |
| G2 | Choose an approach and justify it | Names an approach | Chooses retrieval-augmented generation or fine-tuning with a reason | Compares both, chooses one, and explains the trade-off in cost, accuracy and maintenance |
| G3 | Evaluate output quality | Mentions checking answers | Describes a check, such as sampling answers against the documents | Describes a check against source documents, with a measure of accuracy |
| G4 | Manage risk and data | Mentions risk | Names one risk, such as an incorrect policy answer | Names risks and a control for each, such as citation display and human escalation |

**GAI-2: Judging a summary tool's output.** A summary tool shortens customer calls into notes. A manager asks whether to trust it. Describe how you would judge its output.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| G1 | Frame the problem | Restates the question | Identifies what a good summary must keep | Identifies the facts that must be kept and what counts as an error |
| G2 | Choose an approach and justify it | Names a method | Chooses a comparison against the source calls | Chooses a method, such as sampled comparison with human notes, and gives a reason |
| G3 | Evaluate output quality | Mentions reading the output | Describes a check of facts against the transcript | Describes a sample, the error types measured, and a threshold |
| G4 | Manage risk and data | Mentions risk | Names one risk, such as a missed commitment | Names risks, such as missed commitments or customer data, with a control for each |

**GAI-3: Handling sensitive data in prompts.** Staff want to paste customer records into a language model to draft replies. Advise on what to allow and why.

| ID | Objective | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| G1 | Frame the problem | Restates the request | Identifies that customer data is sensitive | Identifies the data involved, the legal and contractual constraints, and who is affected |
| G2 | Choose an approach and justify it | Names an option | Proposes an approved tool or redaction of identifiers | Compares options, such as redaction, an approved tool, or no use, and chooses with a reason |
| G3 | Evaluate output quality | Mentions checking replies | Describes a human check before sending | Describes the human check and how errors are recorded |
| G4 | Manage risk and data | Mentions privacy | Names a control, such as redaction or access limits | Names risks and controls, including data retention and audit |

---

## 5. Reliability Test Plan

1. Score the reference set with the live model, three runs per response.
2. Compare each objective score with the consensus score: QWK, within-one-level agreement.
3. Check every quotation for verifiability.
4. Run the paired-style and keyword-only sets.
5. Calculate run consistency and routing recall.
6. A skill area is released only when every threshold in section 2 is met for that skill area.

If a threshold is not met, the rubric or prompt is revised and the test repeated. Thresholds are not adjusted to pass a result.

---

## 6. Report and Export Checks

- **Definition checks:** test cases confirm skill proficiency excludes unattempted scenarios, and that scenario, skill and learner reports use the same attempt records.
- **Reconciliation:** each report total is compared with the attempt records. The target is 100% agreement.
- **Export parity:** the CSV and JSON for the same report are compared field by field. The target is 100% agreement.
- **Export completeness:** each exported record must contain every field in the export schema.

---

## 7. Limits of the Evaluation

- With 40 responses per skill area, confidence intervals are wide. Results are reported with bootstrap intervals, and no statistical significance is claimed.
- The reference set is written by the product team, which limits realism.
- Follow-up improvement shows change in scores on practice scenarios; it does not show transfer to work.
