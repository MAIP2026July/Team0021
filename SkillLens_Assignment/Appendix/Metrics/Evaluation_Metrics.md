# SkillLens: Data, Model and Evaluation Strategy

## 1. AI Task Definition

SkillLens performs rubric-based evaluation of short free-text responses. The language model assigns an ordinal score from 0 to 3 for each learning objective and returns a verbatim quotation as evidence. Follow-up scenarios are drawn from the same scenario set, tagged to the objective they test.

The model selects from validated content. It does not define objectives, rubric levels, or the confidence determination.

---

## 2. Defined Terms and Measurement Conventions

| Term | Definition | Measurement method | Target |
|---|---|---|---|
| Agreement with expert consensus | Quadratic weighted kappa (QWK) between the model score and the consensus score for each objective, averaged across objectives | Reference set; consensus from two graders with adjudication | QWK ≥ 0.70 |
| Within-one-level agreement | Share of objective scores within one level of consensus | Reference set | ≥ 85% |
| Human reliability | QWK between the two graders before adjudication | Reference set | QWK ≥ 0.70. If not met, the rubric is revised before the model is evaluated |
| Evidence verifiability | Share of displayed quotations found in the learner's text (case and whitespace normalized) | Automated check on every scored attempt | 100%. Any failure blocks release |
| Run consistency | Share of objective scores identical across the three runs of one attempt | Automated; reported per skill | ≥ 90% identical; no objective differs by two or more levels |
| Routing recall | Share of model errors of two or more levels that fall into the low-confidence category | Reference set | ≥ 80% |
| Paired-style shift | Mean difference in score between a response and its paired rewrite in a different register or language style | Paired-style test set | Mean shift ≤ 0.5 level |
| Group agreement gap | Difference in QWK between writing-style or language groups | Paired-style test set | ≤ 0.10 |
| Keyword-only score | Mean score for responses that list relevant terms without reasoning | Keyword-only test set | ≤ 1 per objective |
| Override rate | Share of reviewed results where the reviewer changes at least one objective score | Production audit log (pilot) | Reported; reviewed at pilot gate |
| Follow-up improvement | Share of follow-up attempts in which the objective score is higher than in the first attempt | Learner records (pilot) | Reported per skill |
| Time to improvement | Days between the first attempt and the first follow-up attempt that improves the objective score | Learner records (pilot) | Reported |
| Authoring effort | Hours to author and validate one skill's content | Content team log | Reported per skill; expected to decline across skills |

---

## 3. Data Sources

| Source | Type | Description | Use |
|---|---|---|---|
| Learning objectives | Internal | 3 to 5 objectives per skill, defined by subject-matter experts | Content model; rubric |
| Scenarios and rubrics | Internal | 5 to 8 scenarios per skill with level descriptors per objective | Scoring |
| Reference set | Created | 40 responses per skill, scored by two graders | Reliability testing |
| Paired-style set | Created | 12 responses rewritten in different registers, with the same expected scores | Bias testing |
| Keyword-only set | Created | 6 responses listing terms without reasoning | Gaming test |
| Learner responses | User-generated | Free-text responses | Scoring (pilot onward; not used in the MVP) |
| Benchmark score | External input | One score per skill and learner | Context for the learner (MVP mock input) |

The Python objectives in this document are defined for the reference skill. They are not Skillsoft's internal objectives.

---

## 4. Reference Set and Ground Truth

1. Responses are written to cover weak, partial and strong quality levels for each scenario.
2. Two graders score each response for each objective, without access to model output.
3. Where graders differ by more than one level, adjudication is recorded with its reason.
4. Human reliability is measured before the model is evaluated.
5. The reference set is extended with paired-style and keyword-only responses.

The MVP reference set is authored by the product team. This limits realism, and the limitation is stated in the final report.

---

## 5. Reference Rubric: Python for Data Analysis

| ID | Objective | Level 0 | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|---|
| O1 | Load and validate data | No checks described | Names checks (data types, duplicates) | Describes a specific check and its result | Checks data types, duplicates and date formats; states the action taken when a check fails |
| O2 | Handle missing and inconsistent values | No handling, or incorrect handling | States "drop" or "fill" without a reason | Selects a method and gives a reason | Selects a method, states its effect on results, and identifies the bias it may introduce |
| O3 | Aggregate correctly | Incorrect denominator or join | Correct aggregation without a check | Correct aggregation with a sanity check | Correct aggregation; verifies the denominator; defines the rate explicitly |
| O4 | Interpret and qualify results | Claims without support | States a figure | Notes one limitation | States the result, its uncertainty, and what it cannot show |

**Scoring rule.** A score above 0 requires a verbatim quotation from the response. Where no supporting text exists, the score is 0 and the quotation is recorded as "none".

---

## 6. Baselines

1. **Benchmark score only.** A single score cannot identify the failed objective. For each reference response, the baseline is assessed on whether it identifies the gap. Expected result: it does not, by design.
2. **Keyword rule matching.** For each objective, a list of expected terms (for Python: `dropna`, `fillna`, `to_datetime`, `duplicated`, `groupby`, `denominator`, `rate`) is matched against the response. This is the low-cost alternative. The model must outperform it on the reference set to justify its use.

---

## 7. Model and Prompt Design

- **Approach.** Hosted language model through an API, with structured JSON output. No fine-tuning in the MVP.
- **Model selection.** Candidate models are compared on the same reference set. The selected model, its version, and the selection date are recorded in the audit trail.
- **Input.** Skill name, scenario, objective descriptors and level rules, and the learner's response.
- **Output (per objective).** Objective identifier, score (0 to 3), quotation (verbatim or "none"), and a one-sentence rationale.
- **Settings.** Temperature 0; three runs per attempt.
- **Prompt rules.** A score requires a verbatim quotation. Where no evidence exists, the score is 0. The model does not infer intent that the learner did not state.
- **Post-processing (code).** Schema validation; quotation check; run comparison for confidence determination.

---

## 8. Launch Thresholds

| Metric | Threshold | Basis |
|---|---|---|
| QWK against consensus | ≥ 0.70 per objective, averaged | Commonly used reliability threshold for automated scoring |
| Within-one-level agreement | ≥ 85% | Tolerance appropriate to a four-level rubric |
| Human reliability | ≥ 0.70 before model evaluation | Confirms the rubric is applied consistently |
| Evidence verifiability | 100% | Any failure blocks release |
| Run consistency | ≥ 90% identical; none differing by two or more levels | Basis for confidence determination |
| Routing recall | ≥ 80% | Large errors must reach a reviewer |
| Paired-style shift | ≤ 0.5 level | Writing style should not change scores |
| Group agreement gap | ≤ 0.10 QWK | No unexplained difference between groups |
| Keyword-only score | ≤ 1 per objective | Keyword use alone should not earn credit |

**Interpretation.** The reference set contains 40 responses per skill. Confidence intervals will be wide. Results are reported with bootstrap intervals, and no statistical significance is claimed.

If a threshold is not met, the rubric or prompt is revised and the evaluation is repeated. Thresholds are not adjusted to pass a result.

---

## 9. Go / No-Go Criteria for Pilot

Proceed to a controlled pilot only when all of the following are met for the reference skill:

1. Agreement thresholds in section 8 are met.
2. 100% evidence verifiability on the reference set.
3. Run consistency and routing recall thresholds are met.
4. Paired-style and keyword-only checks pass.
5. The reviewer workflow has been tested end to end.

---

## 10. Cost and Privacy

- **Cost per attempt.** Three model calls with a short prompt and short structured output. Costs are calculated at the provider's current pricing at build time.
- **Privacy.** Learners are identified by pseudonymous identifiers. Personal names and manager identities are excluded from prompts. Provider data-retention terms are reviewed before any pilot with real employees. Responses are retained only for the pilot period and then deleted.
- **Data minimization.** Scores, quotations and audit metadata are stored. Raw model outputs are retained only where required for audit.
