# SkillLens: Ethics, Governance and Risk Note

This note identifies the risks of SkillLens as an assessment integration point, who could be harmed and how, the controls for each risk, and the conditions under which release must be paused or rejected. It covers the three live skill areas, the reports and exports, and the coming-soon areas when they are released.

The prototype and the reference sets use synthetic content and simulated learner responses. No real learner data has been processed. Where this note describes real use, it describes the controls required before that use.

---

## 1. Main Risks

| ID | Risk | Description |
|---|---|---|
| R1 | Misquoted or unsupported evidence | A score is shown with a quotation that is not in the response, or does not support the score |
| R2 | Inaccurate scoring | The model scores an objective higher or lower than an expert would |
| R3 | Bias against writing style or language | Responses in a different register or in a second language receive lower scores for reasons unrelated to the skill |
| R4 | Gaming of the rubric | Learners use key terms without reasoning and earn credit |
| R5 | Scores used for employment decisions | A development result is used for hiring, promotion, pay or performance rating |
| R6 | Over-reliance on automated results | Partners, managers or learners accept scores without checking the evidence |
| R7 | Exported data reaching the wrong party | Learner-level records are exported to a system or person not authorised to receive them |
| R8 | Reviewer comments containing personal information | A comment shown to a learner discloses personal or sensitive details, or is unfair |
| R9 | Coming-soon areas read as available | A learner or partner starts or relies on an area that has not been reviewed |
| R10 | Feedback that overstates a gap | Feedback implies a skill deficiency the response does not support |
| R11 | Unreliable skill area released | A skill area with a weak rubric or scenario reaches learners or partners |
| R12 | Model provider dependency | A change in the model or its terms alters scores without notice |
| R13 | Partner misuse or misrepresentation | A partner presents SkillLens scores as a performance rating or as a hiring test |

---

## 2. Harm Scenarios

| Risk | Who could be harmed | How |
|---|---|---|
| R1, R2 | Learner | Told that a gap exists where the response shows the skill, or that a real gap is absent |
| R3 | Learners writing in a second language or a different style | Lower scores that reflect style rather than applied skill |
| R4 | Partners and employers | Learners appear competent when they are not |
| R5 | Employee | A development result used in a decision it was not designed to support |
| R6 | Learner and manager | An incorrect result is acted on without review |
| R7 | Learner | Records seen by people who should not see them |
| R8 | Learner | A comment reveals personal information or is unfair |
| R9 | Partner and learner | A coming-soon area is presented as complete |
| R10 | Learner | Feedback that suggests a gap in a specific ability affects their confidence |
| R11 | All learners in the area | Unreliable results reach many people before the problem is found |
| R12 | Partner | Scores change between periods and cannot be compared |
| R13 | Learner | A development score is used as a test result |

---

## 3. Controls

### 3.1 Guardrails

| Risk | Control | Verification |
|---|---|---|
| R1 | Each displayed score requires a quotation. Each quotation is checked against the response. Any failure routes the result to review. | Automated check on every attempt; target 100% verifiable |
| R2 | Three scoring runs per attempt. Runs that disagree are held for review. Each skill area must meet the reliability thresholds before release. | Reference set; QWK ≥ 0.70; within-one-level agreement ≥ 85% |
| R3 | A paired-style test set measures score shifts across registers and language styles. | Mean shift ≤ 0.5 level; group agreement gap ≤ 0.10 QWK |
| R4 | A keyword-only test set measures credit earned from terms alone. Rubrics require reasoning. | Mean keyword-only score ≤ 1 per objective |
| R5 | Every result and export carries the label "Development guidance, not a performance rating." Access to learner records is limited to the learner and their designated reviewer or manager. | Interface and export review before each release |
| R6 | Low-confidence results are held for a reviewer. Every override requires a reason. Reviewer decisions are recorded. | Reviewer override rate reported per skill area |
| R7 | Each export is limited to the integration owner who requested it. Learners are identified by pseudonymous identifiers in exports. The export schema contains only defined fields. | Export access test before each partner pilot; export schema review |
| R8 | Reviewer comments are shown only after review. Reviewers receive guidance on what a comment may contain. Comments that include personal details are rejected before display. | Sample review of comments in each pilot |
| R9 | Coming-soon areas show a yellow tag, cannot be expanded, and have no start action. | Interface review before release |
| R10 | Feedback is drawn only from the rubric descriptor for the next level. It describes the response, not the learner. | Review of feedback text on the reference set |
| R11 | A skill area is released only after its scenarios and rubrics meet the reliability thresholds. | Release gate in the Evaluation Metrics appendix |
| R12 | The model name and version are recorded for every attempt. A model change is treated as an evaluation event: the reference sets are re-run before the change reaches learners. | Audit record; re-evaluation before release |
| R13 | Partner agreements prohibit presenting scores as performance ratings or as test results. The development-guidance label travels with every export. | Contract clause; label check on every export |

### 3.2 Review process

- A reviewer confirms or overrides each held result. Reviewers cannot edit the learner's response.
- Reviewers are trained on the rubric for the skill area before they review its results.
- Overrides require a reason. Repeated overrides on the same objective are sent to the content owner.
- If the review queue grows faster than reviewers can clear it, release to further learners or partners is paused.

### 3.3 Escalation path

| Situation | Action | Owner |
|---|---|---|
| Quotation verification fails | Hold the result; log the failure; notify the product owner if failures recur | Reviewer; product owner |
| Learner disputes a result | Route to a reviewer; if upheld, correct the record and review the rubric | Reviewer; content owner |
| Suspected bias in a group | Pause the affected skill area; re-run the paired-style test; report to the product owner | Evaluation lead |
| Export sent to an unauthorised party | Revoke the export access; notify the partner and the data-protection lead | Product owner |
| Score used outside its purpose | Stop the partner's access to that report; require written confirmation of use | Product owner |
| Privacy incident | Follow the organisation's incident process; notify the data-protection lead | Product owner |

### 3.4 Logging and auditability

Every scored attempt records:
- skill area, scenario and rubric versions;
- model identifier and prompt version;
- the three run outputs and the confidence determination;
- each quotation and its verification result;
- reviewer decisions, reasons, comments and timestamps;
- the export requests and the fields exported.

Logs are kept for the audit period set by the organisation. Learner-identifying information is kept separate from the scoring record.

---

## 4. Risk Register

Likelihood and impact are rated low, medium or high for the pilot. The ratings are judgements and are reviewed after the reference-set results.

| ID | Likelihood | Impact | Residual risk after controls | Owner |
|---|---|---|---|---|
| R1 | Medium | High | Low (automated check blocks unverified display) | Build lead |
| R2 | Medium | High | Medium until reference-set results are available | Evaluation lead |
| R3 | Medium | High | Medium until paired-style results are available | Evaluation lead |
| R4 | Medium | Medium | Low | Evaluation lead |
| R5 | Medium | High | Low if the label and access controls are in place | Product owner |
| R6 | High | High | Medium; depends on reviewer practice | Product owner |
| R7 | Medium | High | Low if export access is limited and the schema is fixed | Build lead |
| R8 | Medium | Medium | Low with comment guidance and pre-display checks | Product owner |
| R9 | Medium | Medium | Low with the coming-soon controls | Product owner |
| R10 | Medium | Medium | Low | Content owner |
| R11 | Medium | High | Low with the per-area release gate | Content owner |
| R12 | Medium | Medium | Low with re-evaluation on model change | Build lead |
| R13 | Medium | High | Low if the partner agreement and label are in place | Product owner |

---

## 5. Launch Blockers

Release or pilot is stopped if any of the following is true:

1. A displayed quotation fails verification on the reference set or in use.
2. A skill area does not reach QWK ≥ 0.70, or human reliability is below 0.70.
3. The paired-style test shows a group agreement gap above 0.10 QWK.
4. Keyword-only responses earn a mean score above 1 on any objective.
5. An export contains fields outside the schema, or reaches a party without an agreement.
6. Learner data is sent to a model provider whose terms have not been reviewed.
7. The development-guidance label is missing from any result or export.
8. Any feature or partner use presents scores as a performance rating, a test result, or a basis for hiring.
9. A coming-soon area is shown as available.
10. Reviewers have not been trained on the rubric for the skill area being released.
11. A model or prompt change has been made without re-running the reference sets.

A blocker is closed only by evidence from a new test run. The threshold is not changed.

---

## 6. Ownership and Review

This note is reviewed before each roadmap gate, and whenever a new skill area, partner, export field or model is proposed. Changes to the scope in the PRD require a new review of this note.
