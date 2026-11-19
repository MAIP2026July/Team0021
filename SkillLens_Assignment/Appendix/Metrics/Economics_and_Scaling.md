# SkillLens: Business, Pricing and Financial Model

This note sets out who buys SkillLens, what it costs to run, how it is priced, what each customer pays, who bears the AI cost, what the business needs in investment, and what the five-year projection shows. All prices and financial figures are planning assumptions, not measured results. Each assumption is listed in section 2 with a code (A1 to A18) so it can be replaced with pilot data.

---

## 1. Value and Customers

SkillLens is an assessment integration point. It scores open-ended responses to scenarios, shows the evidence behind each score, routes uncertain results to a reviewer, and exports results to the systems that need them.

| Customer | Who they are | Value received |
|---|---|---|
| Platform partners | Learning platforms that want an applied-skill assessment without building scoring, review and reporting | An assessment capability inside their product, with reports they can show their own customers |
| Enterprise L&D teams | Organisations that buy skills development directly | Evidence of applied skill by skill area, reviewer decisions, and exports for their own systems |
| Learners and reviewers | People taking scenarios and the managers who review them | Specific feedback on what to practise, and a reviewer for uncertain results |

**Buyers and users.** Platform partners are the main buyers for the first two years, because they have the learners. Enterprise L&D teams are a second channel. Learners and reviewers use the product but do not pay.

---

## 2. Assumptions

| Code | Assumption | Value | Basis |
|---|---|---|---|
| A1 | Input tokens per scoring run | 2,000 | Rubric, scenario, response and instructions |
| A2 | Output tokens per scoring run | 400 | Structured output for four objectives |
| A3 | Scoring runs per attempt | 3 | Confidence rule (PRD section 8) |
| A4 | Model input price | $3 per million tokens | Illustrative; check provider pricing |
| A5 | Model output price | $15 per million tokens | Illustrative; check provider pricing |
| A6 | Model cost per scored attempt | $0.036 | Derived from A1 to A5 |
| A7 | Share of attempts routed to review | 10% | Assumed; falls as rubrics improve |
| A8 | Reviewer time per review | 5 minutes | Assumed |
| A9 | Loaded cost of reviewer time | $40 per hour | Assumed |
| A10 | Hosting, model overhead and support | 15% of revenue | Planning estimate |
| A11 | Price per scored attempt, platform partner | $1.00 | Proposed; to test with partners |
| A12 | Price per scored attempt, enterprise | $1.20 | Proposed; includes admin and single sign-on |
| A13 | Platform fee, platform partner | $36,000 per year | Proposed; includes API, reports, exports and support |
| A14 | Platform fee, enterprise | $24,000 per year | Proposed |
| A15 | Pilot fee | $5,000 per pilot | Up to 5,000 scored attempts, three months |
| A16 | Scored attempts per partner per year | 150,000 | Planning assumption for a mid-sized learning platform |
| A17 | Scored attempts per enterprise per year | 20,000 | 5,000 learners, four attempts, one skill area |
| A18 | Fixed costs by year | Year 1 $1.45M; Year 2 $1.20M; Year 3 $1.60M; Year 4 $1.90M; Year 5 $2.20M | Team, sales, compliance and infrastructure; see section 7 |

---

## 3. Price List

| Item | Price | What it includes |
|---|---|---|
| Platform partner | $36,000 per year, plus $1.00 per scored attempt | API access, scenario, skill and learner reports, CSV and JSON export, partner support |
| Enterprise | $24,000 per year, plus $1.20 per scored attempt | Everything in the partner tier, plus single sign-on, admin roles and audit export |
| Pilot | $5,000 flat | Up to 5,000 scored attempts, one skill area, three months, reporting included |
| Review service (optional) | $5.00 per review | SkillLens reviewers decide held results for customers who do not have their own |
| Authoring add-on (post-MVP) | $4,000 per new skill area | AI-assisted drafting of scenarios and rubrics, with SkillLens subject-matter review |

**Volume discount (proposed for negotiation).** Partners with more than 500,000 scored attempts a year pay $0.80 per attempt above that volume. This is a test price, not part of the base model in section 7.

**Annual contract value examples**

| Customer | Calculation | Annual contract value |
|---|---|---|
| Platform partner, 150,000 attempts | $36,000 + 150,000 × $1.00 | $186,000 |
| Enterprise, 20,000 attempts (one skill area) | $24,000 + 20,000 × $1.20 | $48,000 |
| Enterprise, four skill areas | $24,000 + 80,000 × $1.20 | $120,000 |

---

## 4. Who Pays for AI

The model cost follows each scored attempt, so it is priced into each attempt. The allocation below is the default; each agreement can change it.

| Cost | Who pays by default | Why | Alternative |
|---|---|---|---|
| Model calls for scoring (three runs per attempt) | SkillLens, recovered through the per-attempt price | The product is the scoring service | Customer brings its own model key and pays the provider |
| Reviewer time for held results | The customer, using its own reviewers | Reviews are part of the customer's process | SkillLens reviewers, for the review service fee |
| AI-assisted drafting of scenarios and rubrics | SkillLens, within the authoring add-on | One-off cost per skill area | Customer authors its own content |
| Subject-matter review of AI-drafted content | SkillLens for add-on work; the customer for its own content | Accountable for rubric accuracy | Not applicable |
| Export and report generation | Included in the platform fee | Low marginal cost | Not applicable |

**Why this default.** Pricing per attempt keeps the cost of AI tied to use. Leaving reviews with the customer keeps the human decision inside the customer's process, which the risk note requires for held results. The review service is priced separately so that the cost of reviews is paid by whoever receives the service.

---

## 5. Unit Economics

**Per scored attempt, platform partner (customer runs reviews)**

| Item | Amount |
|---|---|
| Price | $1.00 |
| Model calls (A6) | −$0.036 |
| Hosting, overhead and support (A10: 15% of price) | −$0.15 |
| **Contribution per attempt** | **$0.81** |

**Per scored attempt, enterprise** (price $1.20): contribution is $1.20 − $0.036 − $0.18 = **$0.98**.

**Review service margin.** Ten per cent of attempts are routed to review (A7). At $5.00 per review and $3.33 cost per review (A8, A9), the margin per attempt is 10% × ($5.00 − $3.33) = **$0.17**. The review service adds contribution, but it also adds staffing, which is why it is optional.

---

## 6. Sensitivity

**Price per attempt.** Break-even scored attempts per year, at fixed costs of $1.9M (Year 4 level):

| Price per attempt | Contribution per attempt | Attempts to cover fixed costs |
|---|---|---|
| $0.70 | $0.56 | about 3.4 million |
| $1.00 (base) | $0.81 | about 2.3 million |
| $1.30 | $1.07 | about 1.8 million |

**Routing rate.** Changing the share of attempts routed to review changes only the cost of reviews SkillLens runs. A routing rate above about 20% removes most of the contribution from the review service. A skill area whose routing rate stays above 10% after its first pilot cycle is reviewed before further expansion.

**Sales timing.** A delay of one year in signing partners moves the cumulative break-even from Year 5 to beyond Year 5. This is the largest single risk in section 8.

---

## 7. Five-Year Financial Projection

Assumptions: the partner and enterprise counts in the table, the scored attempts per customer in A16 and A17, and the prices in section 3. Model cost is A6. Hosting, overhead and support is A10. Figures are in US dollars.

| | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|
| Platform partners (year end) | 0 | 3 | 6 | 12 | 18 |
| Enterprise customers (year end) | 0 | 2 | 10 | 20 | 30 |
| Pilot fees | $10,000 | — | — | — | — |
| Platform fees | — | $156,000 | $456,000 | $912,000 | $1,368,000 |
| Usage revenue (scored attempts) | — | $498,000 | $1,140,000 | $2,280,000 | $3,420,000 |
| **Total revenue** | **$10,000** | **$654,000** | **$1,596,000** | **$3,192,000** | **$4,788,000** |
| Scored attempts | 0 | 490,000 | 1,100,000 | 2,200,000 | 3,300,000 |
| Model calls | — | $17,640 | $39,600 | $79,200 | $118,800 |
| Hosting, overhead and support (15%) | $1,500 | $98,100 | $239,400 | $478,800 | $718,200 |
| **Contribution after variable costs** | **$8,500** | **$538,260** | **$1,317,000** | **$2,634,000** | **$3,951,000** |
| Fixed costs (team, sales, compliance, infrastructure) | $1,450,000 | $1,200,000 | $1,600,000 | $1,900,000 | $2,200,000 |
| **Net cash flow** | **−$1,441,500** | **−$661,740** | **−$283,000** | **$734,000** | **$1,751,000** |
| **Cumulative cash** | **−$1,441,500** | **−$2,103,240** | **−$2,386,240** | **−$1,652,240** | **$98,760** |

**Reading the table**
- **Peak cumulative deficit:** about $2.39 million at the end of Year 3.
- **Cumulative break-even:** during Year 5.
- **Year 5 revenue:** $4.8 million, with 48 customers in total.

Fixed costs in Year 1 include the build phases: validation ($0.2M), the MVP build ($0.55M), and paid pilots with SOC 2 preparation ($0.4M), plus sales, compliance and infrastructure. The minimum run-rate for a team that maintains the product is about $650,000 a year (A18 base, used in earlier drafts), which is below the Year 2 figure because the Year 2 figure includes sales and compliance.

---

## 8. Funding Requirement

| Item | Amount |
|---|---|
| Cumulative cash deficit through Year 3 (section 7) | $2.39M |
| Buffer for slower sales, about 25% | $0.61M |
| **Funding requirement** | **$3.0M** |

**Use of funds across Years 1 to 3 (fixed costs):**

| Area | Years 1 to 3 total | Share |
|---|---|---|
| Team and build | $2.10M | 49% |
| Sales and partnerships | $1.30M | 31% |
| Compliance (SOC 2, legal, data protection) | $0.45M | 11% |
| Infrastructure | $0.40M | 9% |

Sales is the largest variable in the timeline, and the buffer protects against a slower first year of partner signings.

**Milestones linked to funding**
1. Reference-set results meeting the thresholds for the first skill area.
2. Two pilots signed, one of which converts to a platform partner contract in Year 2.
3. Three platform partners live by the end of Year 2.

---

## 9. Scaling Constraints

- **Review capacity** limits scale when SkillLens runs reviews. At 10% routing, 10,000 scored attempts create about 1,000 reviews, which is about 83 reviewer hours a year.
- **Latency:** the three scoring runs are sent in parallel. The target is a 95th-percentile response under 10 seconds.
- **Authoring effort** grows with the number of skill areas. Each new skill area needs its scenarios, rubrics and reference set.
- **Governance** effort grows with each new partner, export field, skill area or model change.
- **Provider dependency** affects cost, latency and results. A model change is treated as an evaluation event.
- **Skill currency:** skills change, so scenarios and rubrics are reviewed on a fixed cycle.

SkillLens scales on attempts, content and review. Expansion to a new skill area or partner waits for review capacity and for that skill area's release gate.

---

## 10. Operations

| Area | Implication |
|---|---|
| Partners | Each integration needs an owner for exports, reviewers and the data agreement |
| Content owners | Each skill area needs an owner for its scenarios and rubrics |
| Engineering | Parallel scoring, monitored latency, audit logs and export checks |
| Data protection | Pseudonymised records, retention limits and deletion under each agreement |
| Provider management | Terms, prices and model versions reviewed on a fixed cycle |

---

## 11. Open Items for Pilots

1. Replace each assumption in section 2 with measured values.
2. Test the $1.00 and $1.20 attempt prices and the $36,000 and $24,000 platform fees with at least two platform partners and two enterprises.
3. Agree in each contract who pays for model calls and for reviews.
4. Measure the routing rate and reviewer time per review in the pilot.
5. Confirm the cost of SOC 2 and legal review before the Year 1 budget is final.
