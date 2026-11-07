# SkillLens: Business, Economics and Scaling View

This note sets out how SkillLens creates value, what it costs to run, how the unit economics behave, and what constrains scaling. All cost figures are planning estimates built from stated assumptions and synthetic data. No pricing, usage or cost data from a live deployment exists. Each assumption is listed in section 2 so that it can be replaced with measured values in the pilot.

---

## 1. Monetisation Model

**Proposed model.** An annual licence per skill, priced per assessed learner, with a review allowance included. Two alternatives are noted for comparison.

| Model | Description | Assessment |
|---|---|---|
| Per learner per skill per year (proposed) | Learners are licensed to one skill; a fixed number of assessment attempts and review allowance are included | Predictable revenue for the buyer; aligns with how learning budgets are set |
| Per assessed attempt (usage-based) | Charged per scored attempt | Aligns cost with use, but makes budgets hard to forecast and does not cover review effort |
| Enterprise licence | Flat fee for a whole organisation | Simple to sell; hides the cost of review, which grows with learners |

**Route to market.** If the Skillsoft partnership is confirmed (PRD section 4.6), SkillLens would be sold as an add-on to the Skillsoft platform, and revenue would be shared under terms that are not yet known. If no partnership is confirmed, SkillLens would be sold directly to employers' learning and development teams. The two routes have different margins, and the economics below assume the direct route unless stated otherwise.

---

## 2. Assumptions

All values below are planning assumptions. They are illustrative and must be replaced with measured values from the pilot.

| Ref | Assumption | Value | Basis |
|---|---|---|---|
| A1 | Input tokens per scoring run | 2,000 | Rubric, scenario, response and instructions |
| A2 | Output tokens per scoring run | 400 | Structured output for four objectives, with quotations and reasons |
| A3 | Scoring runs per attempt | 3 | Confidence rule (PRD section 8) |
| A4 | Input price | $3 per million tokens | Illustrative; check current provider pricing |
| A5 | Output price | $15 per million tokens | Illustrative; check current provider pricing |
| A6 | Share of attempts routed to review | 10% | Assumed; falls as rubrics improve |
| A7 | Reviewer time per review | 5 minutes | Assumed |
| A8 | Loaded cost of reviewer time | $40 per hour | Assumed |
| A9 | Attempts per learner per skill per year | 4 | Assumed; one attempt per scenario per quarter |
| A10 | Authoring hours per skill (one-off) | 27 | Scenarios and rubrics (12 h); reference set of 40 responses (7 h to write, 7 h to grade by two people); adjudication (2 h) |
| A11 | Annual refresh of content | 25% of one-off authoring | Assumed; scenarios and rubrics are updated for changing practice |
| A12 | Scenarios per skill | 6 for the reference skill; 5 to 8 in general | PRD section 6 |

---

## 3. Cost Drivers

### 3.1 Model cost per attempt

Per run: (2,000 × $3 + 400 × $15) ÷ 1,000,000 = $0.012.
Per attempt (three runs): $0.036.

### 3.2 Review cost per attempt

Expected review cost per attempt: 10% × 5 minutes × $40 per hour = $0.33.

### 3.3 Other cost drivers

| Cost driver | Basis | Estimate |
|---|---|---|
| Model API | Three runs per attempt | $0.036 per attempt |
| Reviewer time | 10% of attempts routed | $0.33 per attempt |
| Content authoring | 27 hours per skill, one-off | About $1,080 per skill at $40 per hour |
| Content refresh | 25% of one-off authoring each year | About $270 per skill per year |
| Platform, hosting and support | Not estimated in this note | Required before any pricing is set |
| Learner data storage | Pseudonymous records, deleted after pilot | Not estimated in this note |

**Observation.** Reviewer time, not model cost, is the largest variable cost. Under the assumptions above, reviewer time is about 90% of variable cost per attempt. Reducing the routing rate is therefore a higher priority than reducing the cost of model calls.

---

## 4. Unit Economics

### 4.1 Per learner per skill per year

| Component | Calculation | Amount |
|---|---|---|
| Variable cost per attempt | $0.036 + $0.33 | $0.37 |
| Variable cost per learner per skill per year | 4 attempts × $0.37 | $1.48 |
| Authoring cost per learner (1,000 learners on a skill) | ($1,080 + $270) ÷ 1,000 | $1.35 |
| Fully loaded cost per learner per skill per year | $1.48 + $1.35 | $2.83 |

Fully loaded cost excludes platform, hosting, sales, support and overhead, which are not yet estimated.

### 4.2 Break-even price

The minimum price per learner per skill per year to cover the cost above is $2.83. This does not include platform, sales or overhead, so it is a floor, not a viable price.

### 4.3 Value logic for the buyer

The value case depends on how much learning time the diagnosis avoids. Illustrative example:

- A generic course of 30 hours, costed at $40 per hour of learner time, is $1,200 per learner.
- If the diagnosis redirects a learner away from one unnecessary hour of content, the saving is $40 per learner.
- At a price of $50 per learner per skill per year, the buyer breaks even if the diagnosis avoids 1.25 hours of unnecessary content per learner.

This is an illustration. It requires measured data from the pilot: time spent on unneeded content, completion rates, and gap-closure time (the metrics in the Evaluation Metrics appendix).

### 4.4 Sensitivity

The review routing rate (A6) is the main driver of cost. The table shows the fully loaded variable cost per learner per skill per year at three routing rates.

| Routing rate | Review cost per attempt | Variable cost per learner per skill per year |
|---|---|---|
| 5% | $0.17 | $0.81 |
| 10% (base) | $0.33 | $1.48 |
| 20% | $0.70 | $2.81 |

A routing rate of 20% doubles the variable cost. The routing rate therefore has a launch threshold in the operating plan: review volume is tracked per skill, and a skill whose routing rate stays above 10% after its first pilot cycle is reviewed before further expansion.

---

## 5. Scaling Constraints

### 5.1 Review capacity

Review workload grows with learners, not with compute. At the base assumptions:

| Learners | Attempts per year | Reviews per year (10%) | Reviewer hours per year (5 min each) |
|---|---|---|---|
| 1,000 | 4,000 | 400 | 33 |
| 10,000 | 40,000 | 4,000 | 333 |

Review capacity is the binding constraint on scale. Scaling beyond the capacity of the review team would either lengthen the queue or reduce review quality, and both are launch blockers in the Risk Note.

### 5.2 Latency

Each attempt requires three scoring runs. If the runs are sent in parallel, response time is set by the slowest run rather than the sum of all three. A response-time target of 10 seconds at the 95th percentile is proposed for the learner-facing scoring step. This target is not yet measured.

### 5.3 Cost growth

Model cost grows linearly with attempts and has no fixed per-learner component. Authoring cost grows with the number of skills, not learners, so it is spread across users as the platform grows.

### 5.4 Workflow and content complexity

Each new skill adds scenarios, rubrics and a reference set. Authoring effort per skill is a scaling metric in the Evaluation Metrics appendix. If authoring effort does not fall across skills, the cost of expanding the catalogue will remain high.

### 5.5 Governance burden

Each new skill, model change and new use case requires re-evaluation and a review of the Risk Note. Governance effort grows with the number of skills and the number of model providers in use.

### 5.6 Provider dependency

Scoring depends on a hosted model provider. A change in price, terms, availability or model behaviour changes cost and results. Model changes are treated as evaluation events (Risk Note, R10).

### 5.7 Skill currency

Skills change over time. Skillsoft has cited research that about 40% of core workplace skills could change by 2030 (company-cited; not independently verified). Rubrics and scenarios therefore need a regular review cycle, which adds to the content refresh cost in section 3.3.

---

## 6. Operations Implications

| Area | Implication |
|---|---|
| Reviewers | A trained reviewer pool is needed per skill, with rubric training before they review |
| Content owners | Each skill needs an owner who maintains its rubric and scenarios |
| Engineering | Scoring runs must be parallel and monitored; logs must be kept for the audit period |
| Data protection | Pseudonymised records, retention limits, and deletion at the end of each pilot period |
| Provider management | Terms, pricing and model versions reviewed on a fixed cycle |
| Support | Learners who dispute a result are routed to a reviewer within an agreed time |

---

## 7. Scaling Principle

SkillLens scales on content and review, not on compute. Each skill is released only after it meets the reliability thresholds, and the routing rate is kept under control. Expansion to a new skill or a larger audience begins only when review capacity and the release gate for that skill are both in place.

---

## 8. Open Items for the Pilot

1. Replace each assumption in section 2 with measured values.
2. Measure the routing rate per skill, and the reviewer time per review.
3. Confirm the price a buyer will pay, and the value they report from reduced content time.
4. Confirm the route to market and the revenue share, if the Skillsoft partnership proceeds.
5. Estimate platform, hosting and support costs, which are excluded here.
