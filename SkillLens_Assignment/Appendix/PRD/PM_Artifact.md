# SkillLens: Product Requirements Document

| Field | Value |
|---|---|
| Product | SkillLens: Adaptive Competency Diagnostic and Precision Remediation Engine |
| Document | Product Requirements Document, version 1.0 |
| Scope | Any skill that has defined learning objectives. Python for data analysis is the reference skill. |
| Status | Artifact review |

---

## 1. Problem Statement

Employees who complete a skill benchmark receive a proficiency score, but the score does not identify which applied abilities are missing. Learners who score low are typically assigned broad courses of 30 to 40 hours. These courses have low completion rates and often do not address the specific gap. Managers have no calibrated, evidence-based view of applied ability, and multiple-choice assessments measure recall rather than the ability to reason through a realistic situation.

**Decision being improved:** which specific applied abilities a learner lacks, and what the learner should practise next to close each gap.

---

## 2. Product Vision

Turn a skill into an evidence-backed diagnosis of what a learner cannot yet apply, and the shortest practice path to close each gap.

## 3. Jobs to Be Done

| Persona | Job to be done |
|---|---|
| Learner | When I want to build a practical skill, I want to see which applied abilities I am missing and practise those specifically, so that I can close each gap without repeating a full course. |
| Manager (reviewer) | When a learner's result cannot be scored with confidence, I want to see the learner's answer alongside the evidence, so that I can confirm or correct the result with a recorded reason. |

---

## 4. Market Context and Opportunity

### 4.1 Public context

- Skillsoft launched Skill Benchmark Assessments in Percipio in 2022. Learners answer curated question sets aligned to specific skills and receive a Benchmark score. Administrators and managers can view scores by individual and by team. [BusinessWire, March 2022](https://www.businesswire.com/news/home/20220328005585/en/Skillsoft-Launches-New-Assessment-Capability-in-Percipio-to-Accelerate-Critical-Skill-Mastery-and-Close-Enterprise-Skill-Gaps)
- Skillsoft's next-generation Percipio platform became generally available in February 2026, combining skills mapping, assessment, development and measurement in one platform. [BusinessWire, February 2026](https://www.businesswire.com/news/home/20260204242978/en/Skillsoft-Leads-the-Shift-to-Skills-Management-for-Workforce-Readiness)
- Skillsoft reports 994% year-over-year growth in AI-related Skill Benchmark completions between December 2024 and December 2025. This is a company-reported figure. [Barchart](https://www.barchart.com/story/news/1342730/ai-skills-validation-surges-994-as-employees-seek-to-prove-proficiency)

### 4.2 Why current alternatives are insufficient

| Alternative | Limitation |
|---|---|
| Benchmark score only | Indicates the level, not the gap |
| Generic courses | Low completion; may not address the specific gap |
| Manager check-ins | Uncalibrated and inconsistent across managers |
| Multiple-choice assessment | Measures recall; can be gamed |

### 4.3 Why AI, and why not automatically

Open-ended responses to realistic scenarios show applied reasoning. A language model can read such a response, score it against a written rubric for each objective, and quote the text that supports each score. Published studies report a wide range of agreement between language-model and human graders, depending on model, rubric and prompt. Reliability is therefore measured for each rubric before results are shown to learners. The product is designed around confidence routing and evidence verification, not around a single automated score.

### 4.4 Build, buy or API

| Capability | Decision | Rationale |
|---|---|---|
| Scenario and rubric authoring for open-ended assessments | Build | Core differentiator; the assessment method is the contribution of SkillLens |
| Skill courses and benchmark catalogue | Partner (Skillsoft) | Skillsoft already maintains a large catalogue of skills and benchmarks; SkillLens does not rebuild it |
| Delivery, learner platform and reporting | Partner (Skillsoft) | Assumed to be provided by the platform; integration is not yet verified (section 4.6) |
| Rubric scoring | API (hosted language model) | Commodity capability; accessed through a provider |
| Evidence verification and confidence routing | Build | Differentiating; deterministic and auditable |
| Feedback and follow-up practice | Build | Core to remediation; uses rubric descriptors, not external content |

**Main trade-offs.** API dependence brings provider pricing and availability risk, and learner responses leave the organization. Mitigations are pseudonymous identifiers, no personal names in prompts, and review of provider data terms before any pilot with real learners.

### 4.5 First wedge

Python for data analysis, with six curated scenarios, one learner, and one reviewer step. The product is designed so that a new skill is added as content. A second skill with two scenarios is included in the MVP to test that design.

---

### 4.6 Positioning with Skillsoft

Skillsoft already maintains a catalogue of skills, courses and benchmark assessments, and its platform combines skills mapping, assessment and measurement (references 1 and 2). Trade coverage of the 2022 launch describes hundreds of Benchmark Assessments across technology and leadership subjects (reference 6). SkillLens therefore does not need to build a content library. Its proposed role is to add open-ended, rubric-based assessment and remediation to skills that the catalogue currently tests with multiple-choice and matching items.

| Layer | Skillsoft (assumed or public) | SkillLens (proposed) |
|---|---|---|
| Skill catalogue, courses and benchmarks | Provides | Uses |
| Learner platform, delivery and reporting | Provides | Embeds or links |
| Open-ended scenarios for each skill | Benchmark items are multiple-choice and matching | Authors and maintains |
| Rubric level descriptors for each objective | Objectives exist; rubric descriptors not described publicly | Writes and maintains |
| AI evaluation with quotations and confidence | Not described publicly | Provides |
| Feedback and follow-up practice | Not described publicly | Provides |
| Reviewer confirmation and override | Not described publicly | Provides |

**Work to bring one skill into the platform**

1. Map the skill's benchmark objectives to rubric objectives, using the same identifiers.
2. Author five to eight open-ended scenarios, each tagged to the objectives it tests.
3. Write level descriptors (0 to 3) for each objective, and build a reference set of 40 responses graded by two people.
4. Pass the reliability thresholds in the Evaluation Metrics appendix before the skill is released.
5. Connect the scoring service to the platform. This requires an integration agreement and platform access.

**Limitations.** Skillsoft's scoring method is not public, so SkillLens cannot yet state how its results would relate to benchmark scores. Integration feasibility, data-sharing terms and commercial terms are not known and must be confirmed with Skillsoft. The prototype is standalone and does not connect to Skillsoft.

---

## 5. Core Workflow

1. The learner selects a skill from the content library and reviews its objectives.
2. The system presents a curated scenario for the selected skill.
3. The learner submits a free-text response.
4. The system scores each objective from 0 to 3 against the rubric. Each score includes a verbatim quotation from the response.
5. The system verifies each quotation against the response and determines a confidence level for each objective.
6. The learner sees, for each objective, the score, the supporting evidence, and rubric-based feedback on what the next level requires.
7. For each objective scored below 3, the learner can take a follow-up scenario that tests only that objective.
8. The system compares the objective's score across attempts and shows whether it improved.
9. Results with low confidence are held for reviewer confirmation. The learner then sees the reviewed result.

---

## 6. Skill Content Model

Each skill is defined by four content elements. The product logic is the same for every skill.

| Element | Definition | Owner | Python for data analysis (example) |
|---|---|---|---|
| Objectives | 3 to 5 applied abilities that make up the skill | Subject-matter expert | O1 Load and validate data; O2 Handle missing and inconsistent values; O3 Aggregate correctly; O4 Interpret and qualify results |
| Scenarios | 5 to 8 realistic situations that require the objectives; each scenario is tagged to the objectives it tests | Subject-matter expert | A weekly subscription export with mixed date formats, missing plan types, and duplicate records |
| Rubric | Level descriptors (0 to 3) for each objective in each scenario | Subject-matter expert | Defined in the Evaluation Metrics appendix |
| Reference set | Responses scored by two graders, used to test reliability | Product and evaluation team | 40 responses per skill |

A new skill is released only after it passes the reliability thresholds on its own reference set. Authoring effort per skill is tracked as a scaling metric.

---

## 7. Functional Requirements

| ID | Requirement | Acceptance criterion |
|---|---|---|
| FR-01 | The learner selects a skill from the content library. | Every published skill is listed with its objectives, and each skill loads without error. |
| FR-02 | The system presents one scenario per skill, with the objectives it assesses. | Every scenario lists the objectives defined in its rubric. |
| FR-03 | The system stores the learner's response exactly as submitted. | The stored text matches the submitted text in 100% of cases. |
| FR-04 | The system scores each objective from 0 to 3 with a verbatim quotation. | Every score is validated against the output schema. A score without a quotation is recorded as 0. |
| FR-05 | The system verifies each quotation against the response text. | 100% of quotations are verified before display. Failures are routed under FR-08. |
| FR-06 | The system determines confidence per objective from three scoring runs. | Confidence follows the rules in section 8 in 100% of cases. |
| FR-07 | The system displays per-objective scores, evidence and confidence. | Every displayed score includes its verified quotation and confidence level. |
| FR-08 | Results with low confidence are held for review. | No score from a low-confidence result is displayed to the learner before a reviewer decision. |
| FR-09 | The reviewer confirms or overrides each objective score. | An override cannot be saved without a reason. Every decision is recorded with reviewer role and timestamp. |
| FR-10 | The system provides feedback for each objective scored below 3. | Each feedback statement is derived from the rubric descriptor for the next level. No feedback is generated without a descriptor. |
| FR-11 | The system does not score responses under 40 words or responses that are off-topic. | The learner is prompted to expand the response. No scoring request is made. |
| FR-12 | The system records the audit trail for every scored attempt. | Each record stores the skill version, scenario version, rubric version, model identifier, prompt version, and the three run outputs. |
| FR-13 | Every result is labelled as development guidance. | The label appears on every results screen and in every export. |
| FR-14 | The learner can start a follow-up scenario that tests only a selected objective. | The follow-up scenario is drawn from the skill's scenario set and is tagged to that objective. |
| FR-15 | The system shows the change in an objective's score between attempts. | The change is shown only when both attempts are high or medium confidence. |

---

## 8. Confidence and Fallback Logic

Each attempt is scored three times with a fixed prompt and temperature 0. Confidence is determined by the system from the results of those runs and the verification checks. The model does not report its own confidence.

| Level | Condition | Learner view | Route |
|---|---|---|---|
| High | The three runs agree on every objective, and all quotations are verified | Scores, evidence and feedback | None |
| Medium | All quotations are verified, and at least one objective differs by exactly one level across runs | Results with a note that some results were borderline and a follow-up scenario is recommended | Optional follow-up |
| Low | Any quotation is unverified, any objective differs by two or more levels across runs, or the response is off-topic | No score is displayed; the learner is told that a reviewer will confirm the result | Reviewer queue |

**Standing rules**
- No result is presented as a performance rating.
- Results are visible only to the learner and, where configured, the learner's manager.
- A skill is not released to learners until it meets the reliability thresholds in the Evaluation Metrics appendix.
- Benchmark scores, where provided, are shown as context and do not affect scoring.

---

## 9. Feature Prioritization

Effort and confidence describe the team's estimate of build effort and delivery certainty for the MVP.

| Feature | User value | Effort | Delivery confidence | Priority | Rationale |
|---|---|---|---|---|---|
| Rubric-based scoring per objective | High | Medium | Medium | MVP | Core capability under test |
| Evidence quotation and verification | High | Low | High | MVP | Deterministic; supports trust |
| Confidence routing | High | Medium | Medium | MVP | Governs when results are shown |
| Per-objective diagnosis | High | Medium | Medium | MVP | Core learner value |
| Rubric-based feedback per objective | High | Low | Medium | MVP | Turns the diagnosis into direction |
| Follow-up scenario per objective | High | Medium | Medium | MVP | Closes the remediation loop |
| Score change between attempts | High | Low | High | MVP | Measures improvement |
| Reviewer confirm and override | Medium | Medium | High | MVP (minimal) | Required to test routing end to end |
| Second skill added as content | High | Low | Medium | MVP | Tests the skill-agnostic design |
| Full reviewer workflow and audit view | Medium | Medium | High | Pilot | Needed for controlled pilot |
| Skillsoft Percipio integration | High | High | Low | Post-MVP (Phase 2) | Depends on partnership and platform access |
| Micro-course remediation | High | High | Low | Post-MVP | See section 12 |
| Dynamic scenario generation | Medium | High | Low | Post-MVP | Curated scenarios limit variance |
| Manager analytics | Medium | High | Medium | Post-MVP | Not required to validate diagnosis |
| Hiring and candidate screening | Medium | High | Low | Post-MVP | Requires fairness and legal review |

---

## 10. MVP Definition

**Form.** A web application with a skill selector, curated scenarios, a live scoring service, feedback and follow-up scenarios, and a reviewer screen.

**In scope**
- Two skills: Python for data analysis (six scenarios) and a second skill (two scenarios).
- Free-text response entry.
- Per-objective scores from 0 to 3, verified quotations, confidence levels, and rubric-based feedback.
- Follow-up scenario for any objective scored below 3, with the score change shown between attempts.
- Low-confidence path to a reviewer screen, with confirm or override and a required reason.

**Out of scope**
- Micro-courses and course assignment.
- Benchmark item grading.
- Integration with Skillsoft Percipio. The prototype is standalone (section 4.6).
- Hiring and candidate screening.
- Business-track content.
- Manager analytics.
- Dynamic scenario generation.
- Real learner data.

**The MVP establishes**
- The scoring workflow produces verifiable, evidence-based results.
- Confidence routing prevents unreliable results from reaching learners.
- Feedback and follow-up practice produce a measurable change in objective scores.
- The reviewer override path operates end to end.
- A new skill can be added as content without code changes.

**The MVP does not establish**
- Accuracy at scale or across learner populations.
- Whether score improvements on follow-up scenarios transfer to work.
- Integration effort with Skillsoft Percipio or any other learning platform.
- Whether the scenario approach works for the skills in the Skillsoft catalogue.
- Economic viability.
- Whether learners close skill gaps faster than with current remediation.

---

### Prototype limitations (as submitted)

- Scoring is scripted, using keyword cues for each level, not a live language model. The prototype does not measure model accuracy.
- Quotations are taken from the learner's response. Confidence is derived from cue strength in a single pass. The three-run agreement rule in section 8 is not implemented in the prototype.
- The automatic low-confidence route is not triggered by the prototype. The reviewer queue fills only when a learner requests a review.
- The prototype includes two scenarios per skill, against six for Python in the MVP.
- Content is synthetic. The prototype is not a validated assessment.
- The prototype is standalone and does not connect to Skillsoft or to any learner data.

---

## 11. Risks and Controls

| Risk | Control |
|---|---|
| Misquoted or unsupported evidence | Deterministic quotation check; any failure routes the result to review and blocks release |
| Scoring bias against writing style or language | Paired-style test set; score shifts and agreement gaps reported by group |
| Gaming of the rubric through keyword use | Keyword-only test set; rubric requires reasoning and stated trade-offs |
| Improvement that reflects practice on the same scenario, not skill | Follow-up scenarios use different situations for the same objective |
| Scores used for performance decisions | Development-guidance label; access limited to the learner and designated manager |
| Privacy of employee data | Pseudonymous identifiers; no personal names in prompts; provider data terms reviewed before pilot |
| Over-reliance on automated results | Confidence routing; reviewer override with recorded reason |
| Rubric quality differs across skills | Reliability threshold applied to each skill before release |
| Skillsoft partnership or platform access is not granted | Integration cannot proceed | The scoring service is built to run standalone, so the product does not depend on integration |
| Skillsoft's scoring method is not public | Results cannot be reconciled with benchmark scores | Validate results against expert graders, not against benchmark scores |

A full risk assessment is provided in the Risk Note.

---

## 12. Post-MVP Plan: Micro-Courses

After the scenario loop is validated, a later phase can add short micro-courses for objectives that learners repeatedly find difficult. Each would be a slide-based module of about 5 to 6 minutes with narration, followed by a check on the same objective. Authors would mark the hardest objectives when a skill is built, and subject-matter experts would complete a standard template for each one. Each course would be approved, published, and assigned by a manager, and a check after the course would record whether the gap closed. This is deferred because it depends on item-level benchmark data, a course production workflow, and evidence that the scenario loop works first. The design is kept in this plan so that it can be added without changing the scenario-based core.

---

## 13. References

1. Skillsoft. "Skillsoft Launches New Assessment Capability in Percipio to Accelerate Critical Skill Mastery and Close Enterprise Skill Gaps." BusinessWire, 28 March 2022. https://www.businesswire.com/news/home/20220328005585/en/Skillsoft-Launches-New-Assessment-Capability-in-Percipio-to-Accelerate-Critical-Skill-Mastery-and-Close-Enterprise-Skill-Gaps
2. Skillsoft. "Skillsoft Leads the Shift to Skills Management for Workforce Readiness." BusinessWire, 4 February 2026. https://www.businesswire.com/news/home/20260204242978/en/Skillsoft-Leads-the-Shift-to-Skills-Management-for-Workforce-Readiness
3. Barchart. "AI Skills Validation Surges 994% as Employees Seek to Prove Proficiency." https://www.barchart.com/story/news/1342730/ai-skills-validation-surges-994-as-employees-seek-to-prove-proficiency
4. Zhang et al. "SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks." arXiv:2602.12670. https://arxiv.org/abs/2602.12670
5. Automated essay scoring with large language models under holistic and analytic rubrics. arXiv:2604.00259. https://arxiv.org/html/2604.00259v1
6. Training Industry. Coverage of the Skillsoft launch of Skill Benchmark Assessments in Percipio, 2022. https://trainingindustry.com/press-release/measurement-and-analytics/skillsoft-launches-new-assessment-capability-in-percipio-to-accelerate-critical-skill-mastery-close-enterprise-skill-gaps/
