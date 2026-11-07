# SkillLens: Ethics, Governance and Risk Note

This note identifies the risks of SkillLens, who could be harmed and how, the controls that address each risk, and the conditions under which launch must be paused or rejected. It covers the MVP, the Skillsoft integration path described in the PRD (section 4.6), and the post-MVP options.

The prototype and the reference set use synthetic content and simulated learner responses. No real learner data has been processed. Where this note refers to real use, it describes the controls required before any such use.

---

## 1. Main Risks

| ID | Risk | Description |
|---|---|---|
| R1 | Misquoted or unsupported evidence | A score is shown with a quotation that is not in the learner's response, or that does not support the score |
| R2 | Inaccurate scoring | The model scores an objective higher or lower than an expert would, so the learner receives the wrong development guidance |
| R3 | Bias against writing style or language | Responses in a different register, or in non-native English, receive systematically lower scores |
| R4 | Gaming of the rubric | Learners use key terms without reasoning and receive credit they have not earned |
| R5 | Scores used for performance decisions | A development score is used for hiring, promotion, pay or performance rating |
| R6 | Over-reliance on automated results | Managers or learners accept scores without checking the evidence |
| R7 | Privacy of employee data | Responses, names or manager identities are exposed to the model provider or to unauthorised staff |
| R8 | Feedback that overstates the learner's gap | Feedback implies a skill deficiency that the learner's response does not support |
| R9 | Scope creep into hiring or assessment for selection | The product is extended to candidate screening before fairness and legal review |
| R10 | Provider dependency and change | A change in the model or its terms alters scores without notice |
| R11 | Rubric quality differs across skills | A skill is released with a weak rubric, producing unreliable results |

---

## 2. Harm Scenarios

| Risk | Who could be harmed | How |
|---|---|---|
| R1, R2 | Learner | A learner is told a gap exists where the response shows the skill, and spends time on unnecessary practice; or a real gap is missed |
| R3 | Learners who write in a different register or in a second language | Lower scores that reflect writing style rather than applied skill, and lower confidence in their own ability |
| R4 | Organisation | Learners appear to be competent when they are not, and the skill gap remains in the workforce |
| R5 | Employee | A development score is used in a performance or pay decision, which the product was not designed to support |
| R6 | Learner and manager | An incorrect result is confirmed without review, and the learner receives the wrong guidance |
| R7 | Employee | Responses that contain personal or sensitive information are disclosed, or retained longer than intended |
| R8 | Learner | Feedback that suggests a gap in a specific skill affects the learner's confidence |
| R9 | Candidates | A tool designed for development is used to screen them without validation |
| R10 | Learner and organisation | Scores change between periods, and results cannot be compared over time |
| R11 | Learners on that skill | Unreliable results are shown to many learners before the problem is detected |

---

## 3. Controls

### 3.1 Guardrails

| Risk | Control | How it is verified |
|---|---|---|
| R1 | Every displayed score requires a quotation. The system checks that each quotation appears in the learner's response. Any failure routes the result to review. | Automated check on every attempt. The launch threshold is 100% verifiability (Evaluation Metrics, section 8). |
| R2 | Scores are determined from three scoring runs. Results where runs disagree are held for review. The reliability threshold must be met on each skill's reference set before release. | Reference set; QWK ≥ 0.70 against expert consensus; within-one-level agreement ≥ 85% |
| R3 | A paired-style test set measures score shifts between registers and language styles. | Mean shift ≤ 0.5 level; group agreement gap ≤ 0.10 QWK |
| R4 | A keyword-only test set measures how much credit keyword use earns. The rubric requires reasoning and stated trade-offs. | Mean score on keyword-only responses ≤ 1 per objective |
| R5 | Every result is labelled as development guidance, on every screen and in every export. Access is limited to the learner and their designated manager. The product has no export of scores in the MVP. | Interface review; access control test before pilot |
| R6 | Low-confidence results and unverified quotations are held for a reviewer. Reviewers must record a reason for any override. | Reviewer override rate reported in the pilot; repeated overrides on an objective trigger a rubric review |
| R7 | Learners are identified by pseudonymous identifiers. Names and manager identities are excluded from prompts. Responses are deleted after the pilot period. Provider data terms are reviewed before any real use. | Prompt content review; data-retention check against the provider's terms |
| R8 | Feedback is generated only from the rubric descriptor for the next level. It states what the response did not yet show, and does not describe the learner. | Review of feedback text on the reference set |
| R9 | The product is limited to development use. Hiring and candidate screening are excluded until fairness and legal review are complete. | Scope recorded in the PRD (section 9); launch blocker in section 5 |
| R10 | The model name and version are recorded for every attempt. A model change is treated as an evaluation event: the reference set is re-run before the change reaches learners. | Audit record (PRD FR-12); re-evaluation before release |
| R11 | Each skill is released only after it passes the reliability threshold on its own reference set. | Release gate in the Evaluation Metrics appendix |

### 3.2 Review process

- A reviewer confirms or overrides each held result. Reviewers cannot edit the learner's response.
- Reviewers are trained on the rubric for the skill before they review its results.
- Overrides are recorded with a reason. Repeated overrides on the same objective are sent to the content owner.
- Reviewer workload is monitored. If the review queue grows faster than reviewers can clear it, the product must not expand to more learners.

### 3.3 Escalation path

| Situation | Action | Owner |
|---|---|---|
| Evidence verification fails | Hold the result; log the failed quotation; notify the product owner if failures recur | Reviewer; product owner |
| Learner reports an incorrect result | Route to reviewer; if confirmed, correct the record and review the rubric | Reviewer; content owner |
| Suspected bias in a group | Pause the affected skill; re-run the paired-style test; report to the product owner | Evaluation lead |
| Use of scores outside development purpose | Stop the affected access; inform the employing organisation's data protection lead | Product owner |
| Privacy incident | Follow the organisation's incident process; notify the data protection lead | Product owner |

### 3.4 Logging and auditability

Every scored attempt records:
- skill version, scenario version and rubric version;
- model identifier and prompt version;
- the three run outputs and the confidence determination;
- each quotation and its verification result;
- reviewer decisions, reasons and timestamps.

Logs are retained for the audit period set by the organisation. Learner-identifying information is kept separate from the scoring record.

---

## 4. Risk Register

Likelihood and impact are rated on a three-point scale (low, medium, high) for the pilot. Ratings are judgements and will be reviewed after the reference set results.

| ID | Likelihood | Impact | Residual risk after controls | Owner |
|---|---|---|---|---|
| R1 | Medium | High | Low (automated check blocks unverified display) | Build lead |
| R2 | Medium | High | Medium until reference set results are available | Evaluation lead |
| R3 | Medium | High | Medium until paired-style results are available | Evaluation lead |
| R4 | Medium | Medium | Low | Evaluation lead |
| R5 | Medium | High | Low if access controls are in place | Product owner |
| R6 | High | High | Medium; depends on reviewer practice | Product owner |
| R7 | Medium | High | Low if provider terms and pseudonymisation are confirmed | Product owner |
| R8 | Medium | Medium | Low | Content owner |
| R9 | Low | High | Low while scope is limited to development | Product owner |
| R10 | Medium | Medium | Low with re-evaluation on model change | Build lead |
| R11 | Medium | High | Low with per-skill release gate | Content owner |

---

## 5. Launch Blockers

Launch or pilot is stopped if any of the following is true:

1. Any displayed quotation fails verification on the reference set or in use.
2. A skill does not reach QWK ≥ 0.70 against expert consensus, or human-to-human reliability is below 0.70.
3. The paired-style test shows a group agreement gap above 0.10 QWK.
4. Keyword-only responses earn a mean score above 1 on any objective.
5. Scores can be exported or viewed by anyone other than the learner and the designated manager.
6. Learner data is sent to a model provider whose terms have not been reviewed.
7. The development-guidance label is missing from any result screen or export.
8. Any feature uses scores for hiring, pay, promotion or performance rating.
9. Reviewers have not been trained on the rubric for the skill being released.
10. Model or prompt changes have been made without re-running the reference set.

A blocker is closed only by evidence from a new test run, not by changing the threshold.

---

## 6. Ownership and Review

This note is reviewed before each phase gate in the Roadmap, and whenever a new skill, a new model, or a new use is proposed. Changes to the scope in section 1 of the PRD require a new review of this note.
