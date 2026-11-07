# SkillLens: Product Roadmap

Each phase ends with a proof gate. The next phase begins only when its gate is passed. If a gate is not passed, the rubric or prompt is revised and the gate is re-tested. Thresholds are not lowered.

| Phase | Scope | Deliverables | Gate to advance |
|---|---|---|---|
| **Phase 1: MVP** | Two skills: Python for data analysis (six scenarios) and a second skill (two scenarios) | Skill selector; scenario delivery; three-run scoring; quotation verification; confidence routing; per-objective scores and rubric-based feedback; follow-up scenario per objective; score change between attempts; reviewer confirm and override | Launch thresholds met on each skill's reference set; 100% evidence verifiability; reviewer path tested end to end |
| **Phase 2: Controlled pilot** | One team of volunteer learners with their managers as reviewers; standalone, or inside Skillsoft Percipio if a partnership and platform access are confirmed | Full reviewer view with audit log; pseudonymous data handling; feedback on each result | Override rate within the agreed range; learners rate the feedback as useful; score improvement on follow-up scenarios observed; no bias flags in paired-style checks on pilot data; provider data terms approved |
| **Phase 3: Expansion** | Additional skills added as content, including skills from the Skillsoft catalogue; trial of dynamic scenario generation; micro-course option (see below) | Content authoring workflow; reliability check per skill; generated scenarios checked against the same rubric before use | Each new skill passes its reliability check on its own reference set; authoring effort per skill declines across skills |
| **Phase 4: Manager analytics and hiring evaluation** | Manager reporting; evaluation of hiring use | Team-level reporting; hiring study design | Fairness and legal review complete before any high-stakes use |

---

## Post-MVP Option: Micro-Courses

Micro-courses are a deferred option, not part of the MVP or Phase 2. After the scenario loop is validated, short slide-based courses of about 5 to 6 minutes could be added for objectives that learners repeatedly find difficult. Each course would be built from a standard template completed by subject-matter experts, approved, published, and assigned by a manager, with a check on the same objective afterwards. The option is considered in Phase 3, once item-level benchmark data is available and the production workflow has been tested. Its requirements are defined in the PRD, section 12.

---

## Skillsoft Integration Path

Integration is planned as a route to learners, not as a separate course library. The steps are:

1. Confirm partnership, platform access and data-sharing terms with Skillsoft.
2. Connect the scoring service to one skill in the pilot.
3. Extend to further skills by authoring scenarios and rubrics for each, and gating each skill on the same reliability thresholds as the standalone MVP.

Until step 1 is confirmed, the pilot runs standalone.

---

## Dependencies and Risks

| Dependency or risk | Effect | Mitigation |
|---|---|---|
| Reference set takes longer to produce than planned | Phase 1 gate is delayed | Begin authoring early; reference set size fixed at 40 responses per skill |
| Rubric does not reach human reliability | The model cannot be evaluated | Revise the rubric before revising the prompt |
| Scenarios for the second skill take longer to write than planned | The skill-agnostic design is not tested | Keep the second skill to two scenarios; report the result whatever it is |
| Follow-up scenarios do not show real improvement | The remediation loop is not validated | Report the result; revise feedback and scenarios before Phase 2 |
| No pilot volunteers | Phase 2 gate cannot be tested | Test learner and reviewer journeys in Phase 1 with the reference set; state the limitation |
| Provider data terms do not permit learner data | Pilot cannot use real responses | Pilot with synthetic responses; document the limitation |
| Skillsoft partnership or platform access not granted | Integration in Phase 2 cannot proceed | Run the pilot standalone; keep the scoring service independent of the platform |
