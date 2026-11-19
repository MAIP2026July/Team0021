# SkillLens: Product Roadmap

Each phase ends with a proof gate. The next phase begins only when its gate is passed. If a gate is not passed, the rubric or prompt is revised and the gate is re-tested. Thresholds are not lowered.

| Phase | Scope | Deliverables | Gate to advance |
|---|---|---|---|
| **Phase 1: MVP** | Three live skill areas (Data Structures and Algorithms, Communication, Generative AI), each with three scenarios | Skill browser with accordions and scenario cards; scoring with quotations and confidence; feedback and follow-up practice; reviewer queue with confirm, override and comments; scenario, skill and learner reports; CSV and JSON export | Reliability thresholds met on each skill area's reference set; 100% of displayed quotations verifiable; reviewer path tested end to end; exports match report values |
| **Phase 2: Integration pilot** | Two or three partner or enterprise pilots that consume the exports or API; the three coming-soon skill areas drafted | Partner-ready API documentation; reviewer workflow with audit view; pseudonymous data handling; skill content for Docker, Product management and Leadership in draft | Pilot partners use exported data in their own reports; learners rate the feedback as useful; score change on follow-up scenarios observed; no bias flags in paired-style checks; data terms agreed with each partner |
| **Phase 3: Expansion** | Authoring workspace for subject-matter experts with AI-assisted drafting; coming-soon skill areas published after review; partner connector | Authoring workflow with review and publication; reliability check for each new skill area; partner connector | Each new skill area passes its reliability check; authoring effort per skill area declines across skills |
| **Phase 4: Scale and evaluation** | Reporting beyond the MVP; evaluation of further use cases | Team-level analytics; study design for any higher-stakes use | Fairness and legal review complete before any high-stakes use |

---

## Post-MVP Option: Micro-Courses

Micro-courses are a deferred option. After the scenario loop and the partner pilots are validated, short slide-based courses of about 5 to 6 minutes could be added for objectives that learners repeatedly find difficult. Each course would be built from a standard template, approved, and followed by a check on the same objective. This is considered in Phase 4, once item-level data and the production workflow are available.

---

## Dependencies and Risks

| Dependency or risk | Effect | Mitigation |
|---|---|---|
| Reference sets take longer to produce than planned | Phase 1 gate is delayed | Begin authoring early; 40 responses per live skill area |
| Rubric does not reach human reliability | The model cannot be evaluated | Revise the rubric before revising the prompt |
| Scenarios in a skill area are weak or unclear | Scores are not trusted | Subject-matter review of each scenario before release |
| Partners do not use the exports | Integration value is not shown | Pilot with at least two partners; agree report fields before build |
| Partner data terms do not permit learner data | Pilots cannot use real responses | Pilot with synthetic responses until terms are agreed |
| Coming-soon skill areas are read as available | Learners or partners are misled | Yellow tag, no accordion, no start action |
