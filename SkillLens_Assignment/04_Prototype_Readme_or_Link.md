# Prototype: SkillLens

## Prototype Type

Browser prototype. A single HTML file, `Appendix/Prototype/index.html`, that runs without a server, account or network connection. Scoring is scripted, not produced by a live language model. All learners, responses and report values are synthetic.

## What It Demonstrates

**Learner view**
1. A skill browser with three live skill areas (Data Structures and Algorithms, Communication, Generative AI), each shown as an expandable accordion with three scenario cards.
2. Coming-soon skill areas (Docker, Product management, Leadership), marked with a yellow tag.
3. A scenario response of at least 40 words. The system checks length and relevance before scoring.
4. Results for each objective: a score from 0 to 3, the quotation behind it, and feedback on the next level.
5. A scenario score and a skill proficiency, calculated from the latest attempted scenarios only.
6. A follow-up scenario on any objective below 3, with the score change shown.
7. Requests for review, and reviewed results that include any reviewer comment.

**Reviewer view**
1. A review-request queue with the reason for each item.
2. A review screen that shows the learner's response beside the AI scores and quotations. The reviewer confirms or overrides each score, requires a reason for any override, and may add a comment for the learner.
3. An authoring area, shown as coming soon.
4. Scenario and skill reports, and learner reports, with CSV and JSON export. Both formats contain the same fields.

## AI Role

- **In the product design:** a language model scores each objective against a written rubric and returns a verbatim quotation. Confidence is determined by the system from three scoring runs and a quotation check. The model does not report its own confidence.
- **In this prototype:** the AI role is simulated. Each objective has keyword cues for each level, and the quotation is the sentence that contains the cue. This shows the workflow and the screens. It does not show model accuracy.

## What It Does Not Yet Prove

- **Scoring accuracy.** Scoring is scripted. Agreement with expert graders has not been measured, and no reference set has been scored.
- **Confidence routing.** The three-run agreement rule is not implemented. Results are held for review only when a learner requests a review.
- **Coverage.** Three scenarios per live skill area. The coming-soon areas have no content.
- **Content quality.** Scenarios, rubrics, cues and feedback are drafts. They are not validated by subject-matter experts.
- **Learning effect.** The score change on a follow-up scenario does not show improvement at work.
- **Integration.** The API and the CSV and JSON exports are downloadable files. No partner platform is connected.
- **Reports.** The reports use synthetic learners, so the averages show the calculation, not real performance.
- **Fairness.** Writing-style and language groups have not been tested.

## Links

- **Prototype:** `Appendix/Prototype/index.html`
- **Screen recording (no audio), two parts:** `Appendix/Screenshots_or_Video/SkillLens_Demo_LearnerFlow.mov` (learner flow) and `Appendix/Screenshots_or_Video/SkillLens_Demo_reviewerFlow.mov` (reviewer flow)
- **Wireframes:** `Appendix/Wireframes/`, with the screen specifications in `Appendix/Wireframes/UX_and_Workflow_Specification.md`
- **Workflow:** `Appendix/Workflow/`, with the swimlane diagram and the workflow description

## Setup

No setup is needed. Open `Appendix/Prototype/index.html` in a current version of Chrome, Edge, Firefox or Safari.
