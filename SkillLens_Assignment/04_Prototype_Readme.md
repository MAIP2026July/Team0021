# Prototype: SkillLens

## Prototype Type

Browser prototype. A single HTML file (`SkillLens_Assignment/Prototype/index.html`) that runs without a server, account or network connection. Scoring is scripted, not produced by a live language model.

## What It Demonstrates

The core learner and reviewer loop for open-ended assessment:

1. A learner selects a skill and a scenario and writes a response.
2. The system scores each objective from 0 to 3, showing the quotation that supports each score.
3. Each objective below 3 shows feedback on what the next level requires.
4. The learner takes a follow-up scenario on one objective, and the score change is shown.
5. A reviewer can confirm or override a result. An override requires a reason, and the learner then sees the reviewed result.

The prototype covers two skills (Python for data analysis and communication skills), with two scenarios each.

## AI Role

- **In the product design:** a language model scores each objective against a written rubric and returns a verbatim quotation. Confidence is determined by the system from repeated scoring runs and a quotation check. The model does not report its own confidence.
- **In this prototype:** the AI role is simulated. Each objective has keyword cues for each level, and the quotation is the sentence that contains the cue. This shows the workflow and the screens. It does not show model accuracy.

## What It Does Not Yet Prove

- **Scoring accuracy.** Scoring is scripted. Agreement with expert graders has not been measured, and no reference set has been scored.
- **Confidence routing.** Confidence is based on cue strength in one pass. The three-run agreement rule is not implemented. The automatic low-confidence route is not triggered, so the reviewer queue fills only when a learner requests a review.
- **Coverage.** Two scenarios per skill are included, against six for Python in the MVP.
- **Content quality.** Scenarios, rubrics and feedback are synthetic. They are not validated by subject-matter experts.
- **Learning effect.** The follow-up score change does not show that learners improve at work.
- **Integration.** The prototype is standalone. It does not connect to Skillsoft Percipio or to any learner data.
- **Fairness.** Writing style and language groups have not been tested.

## Links

- **Repository:** this repository, folder `SkillLens_Assignment/Prototype/` (file `index.html`)
- **Screen recording:** `SkillLens_Assignment/Appendix/ScreenRecording/PrototypeSkillLens.mov`. The recording has no audio. The readme in the same folder lists the inputs used and their expected results.
- **Screenshots and wireframes:** `SkillLens_Assignment/Appendix/Wireframes/`

## Setup

No setup is needed. Open `SkillLens_Assignment/Prototype/index.html` in a web browser.
