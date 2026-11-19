# SkillLens: Product Requirements Document

| Field | Value |
|---|---|
| Product | SkillLens: open-ended skills assessment, delivered as an integration point for learning platforms |
| Document | Product Requirements Document |
| Scope | Three live skill areas with three scenarios each; three further skill areas marked coming soon |
| Status | Artifact review |

---

## 1. Problem Statement

Learning platforms and enterprises assess skills with multiple-choice and matching items. These formats measure recall. They do not show whether a person can apply a skill to a realistic situation, and they do not say which applied ability is missing. Learners who score low are usually assigned broad content of 30 to 40 hours, which has low completion and often does not address the gap. Managers and L&D teams therefore have no calibrated, evidence-based record of applied ability that they can use or share.

**Decision being improved:** which applied abilities a learner lacks in each skill area, and what the learner should practise next.

---

## 2. Product Vision

SkillLens is an assessment layer that any learning platform or enterprise can plug into. It scores open-ended responses to realistic scenarios, shows the evidence behind each score, routes uncertain results to a human reviewer, and exports results to the systems that need them.

---

## 3. Users and Jobs to Be Done

| Role | Who | Job to be done |
|---|---|---|
| Learner | Employee or learner on a partner platform | When I want to build a practical skill, I want to see which applied abilities I am missing and practise those, so that I can close each gap without repeating a full course. |
| Reviewer | Manager or L&D reviewer | When a result cannot be scored with confidence, I want to see the answer and the evidence, so that I can confirm or correct the result with a recorded reason. |
| Integration owner | Platform partner or enterprise L&D administrator | When my learners complete assessments, I want their results in my own systems, so that my reports and decisions use applied-skill evidence. |

Buyers are platform partners (for example, learning platforms that want an open-ended assessment capability) and enterprise L&D teams that use SkillLens directly.

---

## 4. Market Context and Opportunity

### 4.1 Public context

- Skillsoft launched Skill Benchmark Assessments in Percipio in 2022. Learners answer curated question sets aligned to specific skills and receive a Benchmark score. [BusinessWire, March 2022](https://www.businesswire.com/news/home/20220328005585/en/Skillsoft-Launches-New-Assessment-Capability-in-Percipio-to-Accelerate-Critical-Skill-Mastery-and-Close-Enterprise-Skill-Gaps)
- Skillsoft's next-generation Percipio platform became generally available in February 2026, combining skills mapping, assessment, development and measurement. [BusinessWire, February 2026](https://www.businesswire.com/news/home/20260204242978/en/Skillsoft-Leads-the-Shift-to-Skills-Management-for-Workforce-Readiness)
- Skillsoft reports 994% year-over-year growth in AI-related Skill Benchmark completions. This is a company-reported figure. [Barchart](https://www.barchart.com/story/news/1342730/ai-skills-validation-surges-994-as-employees-seek-to-prove-proficiency)
- Public material does not describe how benchmark scores are calculated. SkillLens does not depend on that method.

These sources show that platforms are investing in skills assessment and AI skill validation. They do not establish demand for an open-ended assessment service, which is a hypothesis to test with partners.

### 4.2 Why current alternatives are insufficient

| Alternative | Limitation |
|---|---|
| Score-only assessment | Shows the level, not the gap |
| Generic content | Low completion; may not address the specific gap |
| Manager check-ins | Uncalibrated and inconsistent |
| Multiple-choice and matching items | Measure recall; can be gamed |

### 4.3 Why AI, and why not automatically

Open-ended responses show applied reasoning, such as a trade-off explained or a result checked. A language model can read a response, score it against a written rubric for each objective, and quote the text behind each score. Published studies report a wide range of agreement between language-model and human graders, depending on model, rubric and prompt. Reliability is therefore measured for each rubric before results reach learners, and confidence is routed to a reviewer.

### 4.4 Positioning and build, buy or partner

| Capability | Decision | Rationale |
|---|---|---|
| Scenario, objective and rubric content | Build | Core differentiator |
| Scoring with evidence and confidence | Build, using a hosted language model through an API | The model is a commodity input; the evidence and confidence design is the product |
| Review workflow and reports | Build | Required for trust and for partner reporting |
| Skill courses, learner accounts and delivery | Partner or existing platform | Learning platforms already provide these |
| Export to partner systems | Build (JSON API and CSV) | Makes SkillLens usable as an integration point |

**Trade-offs.** Dependence on a model provider brings price and availability risk. Learner responses leave the organisation when the model is called. Mitigations are pseudonymous identifiers, no personal names in prompts, and review of provider data terms before any pilot with real learners.

### 4.5 First release

Three live skill areas, each with three scenarios: Data Structures and Algorithms, Communication, and Generative AI. Three further skill areas (Docker, Product management, Leadership) are shown as coming soon.

---

## 5. Product Structure

### 5.1 Skill catalogue

| Skill area | Status | Scenarios | Objectives |
|---|---|---|---|
| Data Structures and Algorithms | Live | DSA-1 The High-Traffic Flash Sale; DSA-2 Degrees of Separation; DSA-3 The Rate Limiter for API Protection | O1 Choose the data structure; O2 Analyse time complexity; O3 Analyse space complexity; O4 Explain trade-offs and limits |
| Communication | Live | COM-1 Project delay message; COM-2 Explaining a report format; COM-3 Handling a challenge from a senior stakeholder | C1 Structure the message; C2 Adapt to the audience; C3 Handle questions and challenge; C4 Write concisely |
| Generative AI | Live | GAI-1 Choosing an approach for a support assistant; GAI-2 Judging a summary tool's output; GAI-3 Handling sensitive data in prompts | G1 Frame the problem; G2 Choose an approach and justify it; G3 Evaluate output quality; G4 Manage risk and data |
| Docker | Coming soon | None yet | None yet |
| Product management | Coming soon | None yet | None yet |
| Leadership | Coming soon | None yet | None yet |

The scenarios, objective descriptors and scoring cues for each live skill area are held as skill-pack data, and are reviewed before release. Scenario texts and rubrics are listed in the Evaluation Metrics appendix.

### 5.2 Scores

- **Objective score:** 0 to 3, with a verbatim quotation for each score above 0.
- **Scenario score:** the average of the four objective scores for that scenario, from 0 to 3.
- **Scenario score (latest):** the score from the learner's most recent attempt at that scenario.
- **Skill proficiency:** the average of the latest scenario scores for the scenarios in that skill area that the learner has attempted. Scenarios not yet attempted are not counted; a skill shows "2 of 3 scenarios attempted" until all three are attempted.
- **Improvement:** the difference between the first and latest score for the same scenario or skill.

### 5.3 Authoring

Authoring (creating scenarios and rubrics, including AI-assisted drafting for subject-matter experts) is shown in the reviewer area as coming soon. In this release, skill-pack content is written and reviewed outside the product.

---

## 6. Core Workflows

### 6.1 Learner

1. The learner opens the skill browser. Skill areas are shown as expandable accordions in one common layout; coming-soon skill areas are marked with a yellow "Coming soon" tag and cannot be expanded.
2. The learner expands a skill area and sees a card for each scenario, with its focus, estimated time, latest score and a Start or Retake action.
3. The learner opens a scenario, reads it and the objectives it assesses, and writes a response of at least 40 words.
4. The system checks the response is long enough and on topic, then scores each objective with a quotation.
5. The system verifies each quotation and sets a confidence level for each objective.
6. The learner sees the scenario score, the objective scores with evidence, feedback on the next level, and the skill proficiency with the number of scenarios attempted.
7. For any objective below 3, the learner can practise that objective with a follow-up scenario and sees the score change.
8. Results held for review are shown as pending. When a reviewer decides, the learner sees the reviewed result and any reviewer comment.

### 6.2 Reviewer

1. The reviewer opens the review queue, which lists learner requests and results held for low confidence.
2. The reviewer opens an item and sees the learner's response beside the AI scores, quotations, verification status and run agreement.
3. The reviewer confirms or overrides each objective score. An override requires a reason.
4. The reviewer may add a comment for the learner. Comments are shown on the learner's result.

### 6.3 Integration owner and reports

1. Reports are available in three views:
   - **Scenario report:** attempts per scenario, average latest score, and average score per objective.
   - **Skill report:** learners attempted each skill area, average skill proficiency based on each learner's latest scenario scores, and average number of scenarios attempted per learner.
   - **Learner report:** for each skill and scenario, the first score, the latest score, the change, and the reviewer comment where one exists.
2. Each report can be downloaded as CSV, and the same data is available as JSON through an API. Both use the same fields.

---

## 7. Functional Requirements

| ID | Requirement | Acceptance criterion |
|---|---|---|
| FR-01 | The learner sees all skill areas in one common accordion layout, with no featured skill area. | Every live skill area expands to show its scenario cards. |
| FR-02 | Coming-soon skill areas are shown with a yellow "Coming soon" tag and no accordion. | Coming-soon areas cannot be expanded or started. |
| FR-03 | Each scenario card shows its title, focus, estimated time and the learner's latest score or "Not attempted". | Each card displays all four fields. |
| FR-04 | The system stores the learner's response exactly as submitted. | Stored text matches submitted text in 100% of cases. |
| FR-05 | The system scores each objective from 0 to 3 with a verbatim quotation for each score above 0. | Output validates against the schema. A score without a quotation is recorded as 0. |
| FR-06 | The system verifies each quotation against the response text. | 100% of displayed quotations are verified; failures are routed to review. |
| FR-07 | The system sets confidence per objective from three scoring runs. | Confidence follows section 8 in every case. |
| FR-08 | Results with low confidence are held for review and show no score to the learner. | No held score is displayed before a reviewer decision. |
| FR-09 | The reviewer confirms or overrides each objective score. An override requires a reason. | Overrides without a reason cannot be saved. |
| FR-10 | The reviewer can add a comment that is shown to the learner. | Comments appear on the learner's result after review. |
| FR-11 | The system gives feedback for each objective scored below 3, derived from the rubric descriptor for the next level. | Every feedback item references a rubric descriptor. |
| FR-12 | The system computes scenario scores and skill proficiency as defined in section 5.2. | Calculated values match the definitions in 100% of test cases. |
| FR-13 | The learner can practise any objective below 3 with a follow-up scenario on that objective and sees the score change. | Change is shown only when both attempts are high or medium confidence. |
| FR-14 | The system provides the scenario, skill and learner reports defined in section 6.3. | Each report displays its defined fields. |
| FR-15 | Each report can be exported as CSV and JSON with the same fields. | The CSV and JSON exports contain identical field values. |
| FR-16 | The system records an audit trail for every scored attempt. | Each record stores skill, scenario and rubric versions, model identifier, prompt version, the three run outputs, quotation checks, and reviewer decisions. |
| FR-17 | Every result and export carries the label "Development guidance, not a performance rating." | The label appears on every results screen and export. |
| FR-18 | The system does not score responses under 40 words or responses that are off-topic. | The learner is asked to expand or revise, and no scoring request is made. |
| FR-19 | Authoring is visible in the reviewer area as coming soon, with its purpose described. | The authoring area has no working controls in this release. |

---

## 8. Confidence and Fallback Logic

Each attempt is scored three times with a fixed prompt at temperature 0. The system determines confidence from the three runs and the quotation check. The model does not report its own confidence.

| Level | Condition | Learner view | Route |
|---|---|---|---|
| High | The three runs agree on every objective, and all quotations are verified | Scores, evidence and feedback | None |
| Medium | All quotations verified; at least one objective differs by one level across runs | Results with a note that some were borderline; optional follow-up | Optional follow-up |
| Low | Any quotation unverified; any objective differs by two or more levels; response off-topic | No score shown; the result is held | Reviewer queue |

**Standing rules**
- No result is presented as a performance rating.
- Results are visible to the learner and, where the integration owner has configured it, to the learner's manager.
- A skill area is not released to learners until its scenarios meet the reliability thresholds in the Evaluation Metrics appendix.

---

## 9. Feature Prioritisation

| Feature | Value | Effort | Priority | Rationale |
|---|---|---|---|---|
| Skill browser with accordions and scenario cards | High | Low | MVP | Core learner navigation |
| Scoring with quotations, verification and confidence | High | Medium | MVP | Core capability under test |
| Feedback and follow-up practice | High | Medium | MVP | Turns diagnosis into practice |
| Reviewer queue, confirm and override | High | Medium | MVP | Required for low-confidence results |
| Reviewer comments shown to learners | Medium | Low | MVP | Adds reviewer value |
| Scenario, skill and learner reports | High | Medium | MVP | Required by integration owners |
| CSV and JSON export | High | Low | MVP | Makes SkillLens an integration point |
| Authoring (coming soon, AI-assisted drafting) | High | High | Post-MVP | Needs reviewed drafting workflow |
| Docker, Product management, Leadership skill areas | Medium | Medium each | Post-MVP | Content authoring and review |
| Learning-platform integration (partner connector) | High | High | Post-MVP | Depends on a partner agreement |
| Manager analytics beyond reports | Medium | Medium | Post-MVP | Not needed to validate the assessment |
| Hiring and candidate screening | Medium | High | Excluded | Requires fairness and legal review |

---

## 10. MVP Definition

**Form.** A web application with a skill browser, scenario responses, results and follow-up, a reviewer queue, reports, and CSV and JSON export. The prototype is a single browser page with synthetic data.

**In scope**
- Three live skill areas, each with three scenarios and four objectives.
- Scoring, quotation verification, confidence routing and reviewer decisions.
- Reviewer comments shown to learners.
- Scenario, skill and learner reports with CSV and JSON export.
- Coming-soon presentation for three skill areas and for authoring.

**Out of scope**
- Authoring tools, beyond the coming-soon placeholder.
- The three coming-soon skill areas.
- A production partner connector and identity integration.
- Hiring and candidate screening.
- Real learner data.

**The MVP establishes**
- Open-ended responses produce evidence-backed scores with a known confidence level.
- Low-confidence results never reach learners before review.
- Practice on an objective produces a measurable score change.
- Reports and exports carry the same fields, so a partner can use them directly.

**The MVP does not establish**
- Accuracy at scale or across learner populations.
- Whether practice changes performance at work.
- Integration effort with any specific partner platform.
- Economic viability.

---

## 11. Risks and Controls

| Risk | Control |
|---|---|
| Misquoted or unsupported evidence | Quotation check; failures routed to review |
| Scoring errors | Reliability thresholds per skill area before release |
| Bias against writing style or language | Paired-style test; group gap reported |
| Gaming of the rubric through keywords | Keyword-only test; rubric rewards reasoning |
| Scores used for performance decisions | Development-guidance label on every result and export |
| Exported data reaching the wrong system | Export access limited to the integration owner; pseudonymous identifiers |
| Reviewer comments containing personal information | Comment guidance for reviewers; comments checked before release |
| Coming-soon areas mistaken for available content | Yellow tag, no accordion, no start action |
| Dependence on a model provider | Provider abstraction; re-evaluation on any model change |

The full risk assessment is in the Risk Note.

---

## 12. Post-MVP Plan

- **Authoring:** a subject-matter-expert workspace in which scenarios, objectives and rubrics are drafted with AI assistance and then reviewed and published.
- **Coming-soon skill areas:** Docker, Product management and Leadership, each published only after it meets the reliability thresholds.
- **Partner connector:** a live integration with a learning platform, under a partner agreement.
- **Micro-courses:** a deferred option for objectives learners repeatedly find difficult. Each would be a short slide-based module with a check on the same objective. Considered only after the scenario loop and the partner connector are validated.

---

## 13. References

1. Skillsoft. "Skillsoft Launches New Assessment Capability in Percipio to Accelerate Critical Skill Mastery and Close Enterprise Skill Gaps." BusinessWire, 28 March 2022. https://www.businesswire.com/news/home/20220328005585/en/Skillsoft-Launches-New-Assessment-Capability-in-Percipio-to-Accelerate-Critical-Skill-Mastery-and-Close-Enterprise-Skill-Gaps
2. Skillsoft. "Skillsoft Leads the Shift to Skills Management for Workforce Readiness." BusinessWire, 4 February 2026. https://www.businesswire.com/news/home/20260204242978/en/Skillsoft-Leads-the-Shift-to-Skills-Management-for-Workforce-Readiness
3. Barchart. "AI Skills Validation Surges 994% as Employees Seek to Prove Proficiency." https://www.barchart.com/story/news/1342730/ai-skills-validation-surges-994-as-employees-seek-to-prove-proficiency
4. "SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks." arXiv:2602.12670. https://arxiv.org/abs/2602.12670
5. "LLM Essay Scoring Under Holistic and Analytic Rubrics: Prompt Effects and Bias." arXiv:2604.00259. https://arxiv.org/html/2604.00259v1
6. Training Industry. Coverage of the Skillsoft launch of Skill Benchmark Assessments in Percipio, 2022. https://trainingindustry.com/press-release/measurement-and-analytics/skillsoft-launches-new-assessment-capability-in-percipio-to-accelerate-critical-skill-mastery-close-enterprise-skill-gaps/
