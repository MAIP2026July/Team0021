# SkillLens: UX, Workflow and Trust Design

This specification defines the screens, states, content and behaviour of the SkillLens MVP. It covers two roles: the learner, who practises open-ended scenarios, and the reviewer, who checks held results and reads reports. The wireframe images in this folder follow the screen identifiers below.

The live skill areas are Data Structures and Algorithms, Communication, and Generative AI. Each has three scenarios. Docker, Product management and Leadership are shown as coming soon.

---

## 1. Design Principles

1. **Review assistant, not an authority.** No score is shown without the evidence behind it.
2. **Development guidance, not a rating.** Every result and export carries this label.
3. **Human review where confidence is low.** A held result is never silently withheld; the learner is told what happens next.
4. **One layout for every skill area.** No skill area is featured or highlighted.
5. **Plain language.** Labels are written for a non-specialist reader.

---

## 2. Screen Inventory

| ID | Screen | Role | Purpose |
|---|---|---|---|
| B0 | Browse skills | Learner | Expand skill areas and see scenario cards; see coming-soon areas |
| S1 | Scenario and response | Learner | Read the scenario and objectives; write and submit a response |
| S2 | Results | Learner | Scenario score, objective scores with evidence, feedback, and skill proficiency |
| S3 | Pending review | Learner | Explain that a reviewer will confirm the result |
| S5 | Reviewed result | Learner | Show the reviewed scores, status and any reviewer comment |
| S6 | Follow-up and score change | Learner | Show a follow-up on one objective and the change from the first attempt |
| R1 | Review requests | Reviewer | Queue of learner requests and held results |
| R2 | Review decision | Reviewer | Confirm or override each score; add an optional comment for the learner |
| R3 | Authoring (coming soon) | Reviewer | Placeholder describing the planned authoring workspace |
| R4 | Scenario and skill report | Reviewer | Report by scenario and by skill area; CSV and JSON export |
| R5 | Learner report | Reviewer | Report by learner; CSV and JSON export |

---

## 3. Screen Specifications

### B0: Browse skills

- Heading: "Browse skills".
- One accordion per live skill area, in one common layout, with no featured item. Each accordion row shows the skill area name, the number of scenarios, and the learner's skill proficiency with "n of 3 scenarios attempted", or "Not yet attempted".
- Expanded accordion: one card per scenario. Each card shows the scenario title, a one-line focus, the estimated time, the latest score for that scenario (or "Not attempted"), and a Start or Retake button.
- Coming-soon skill areas (Docker, Product management, Leadership) are listed as rows with a yellow "Coming soon" tag. They have no chevron and no action.
- Footer: development-guidance statement.

### S1: Scenario and response

- Header: skill area name and scenario number (for example, "Generative AI · Scenario 2 of 3").
- Scenario title and text.
- Objectives panel: the four objectives assessed, listed by name before the response.
- Response field: free text, with a word count.
- Validation: responses under 40 words show a prompt to expand. Submission is not blocked, but no score is requested.
- Primary action: Submit, disabled until at least one character is entered.

### S2: Results

- Scenario score (average of the four objectives), with the confidence label (High or Medium).
- Objective table or cards, one per objective, with: name; score (for example, "2 of 3"); the verbatim quotation from the response; and, for scores below 3, a line titled "To reach the next level" with the descriptor for the next level.
- Objectives below 3 show a "Practise this objective" action, which starts a follow-up scenario on that objective.
- Skill proficiency panel: the skill area's proficiency as the average of the latest scores of its attempted scenarios, with the note "Based on 2 of 3 scenarios attempted. Scenarios not yet attempted are not counted."
- Medium confidence shows the banner: "Some results were borderline. A second scenario would give a more reliable picture."
- Secondary action: Request review.
- Footer: development-guidance statement.

### S3: Pending review

- Heading: "A reviewer will confirm this result."
- Body: "No score is shown until a reviewer has checked it. Your response has been saved."
- Status: Pending review, with the submission date and time.
- No scores, objective breakdown or feedback are shown.

### S5: Reviewed result

- Status line: "Reviewed on [date] by reviewer. Scores: confirmed" or "Scores: adjusted by reviewer."
- Scores and feedback as in S2, using the reviewed values.
- Reviewer comment, if one was given, shown in a labelled box titled "Reviewer comment".

### S6: Follow-up and score change

- Heading: the objective name.
- First attempt score and follow-up score, with the change in levels (for example, "Up 1 level").
- The change is shown only when both attempts are high or medium confidence. Otherwise the follow-up is shown with the message that a reviewer will confirm it.
- Evidence and one line of feedback for the follow-up.
- Actions: "Practise another objective" and "Done".

### R1: Review requests

- Top navigation: Review requests, Authoring (coming soon), Reports.
- Filters: skill area and status.
- Table columns: learner (pseudonymous identifier), skill area, scenario, submitted, reason (low confidence, unverified quotation, or learner request), status (pending, confirmed, overridden), and an action "Review" for pending rows.

### R2: Review decision

- Left panel: the learner's response, with the cited quotations highlighted.
- Right panel: AI scores per objective, the quotations, verification status and run agreement.
- Decision per objective: Confirm, or Override with a score from 0 to 3.
- Reason for override: required when any score is overridden.
- Comment for learner: optional, shown to the learner after review. Guidance is shown beside the field: "Do not include personal details."
- Actions: Save decision (primary) and Cancel.

### R3: Authoring (coming soon)

- Yellow "Coming soon" tag and the heading "Authoring".
- Text: "SMEs can generate open-ended scenarios using AI, based on a skill and its objectives, and set evaluation rubrics."
- Greyed-out form outline with fields "Skill", "Objectives" and "Scenario", and a greyed "Generate scenario" button. No working controls.

### R4: Scenario and skill report

- Two tables.
- **By skill area:** skill area, learners attempted, average skill proficiency (latest scenario scores), average scenarios attempted per learner.
- **By scenario:** skill area, scenario, attempts, average latest score, and the average for each of the four objectives.
- Actions: Export CSV and Export JSON. Both export the same fields.

### R5: Learner report

- Learner selector (pseudonymous identifier).
- Table columns: skill area, scenario, first attempt score, latest attempt score, change, and reviewer comment.
- Summary row per skill area: skill proficiency with the number of scenarios attempted.
- Actions: Export CSV and Export JSON.

---

## 4. Uncertainty and Fallback States

| State | Learner sees | System behaviour |
|---|---|---|
| High confidence | Scores, evidence, feedback, skill proficiency | Shows the result |
| Medium confidence | Scores with borderline banner and follow-up option | Shows the result; records the attempt for reliability analysis |
| Low confidence | Pending review screen (S3) | Holds the result; adds it to the review queue |
| Unverified quotation | Same as low confidence | Holds the result; logs the failed quotation |
| Under 40 words or off-topic | Prompt to expand or revise | No scoring request is made |
| Scoring service unavailable | Message to retry; response saved | Retries once; shows no partial result |
| Coming-soon skill area selected | Not available | Cannot be opened |

---

## 5. Trust and Explainability

| Element | Visible to learner | Hidden from learner |
|---|---|---|
| Development-guidance label | Yes, on every result | Not applicable |
| Method description | Yes, in a short expandable note | Model name, prompt text, technical parameters |
| Evidence | Verbatim quotations | Raw model output |
| Confidence | High or Medium label | Numeric values |
| Review status | Yes, with date | Reviewer identity |
| Reviewer comment | Yes, when given | Comments not approved for display |

---

## 6. Human-in-the-Loop

- **Entry points for review:** low-confidence results, unverified quotations, and learner requests.
- **Reviewer actions:** confirm each objective score, or override it with a required reason, and add an optional comment for the learner.
- **Reviewer limits:** cannot edit the learner's response, see other learners' responses outside the queue, or export data beyond the reports they are permitted to see.
- **Escalation:** repeated overrides on the same objective are sent to the content owner.

---

## 7. Accessibility and Content Standards

- Every function is available by keyboard. Accordions use native disclosure controls, so they work with a keyboard and a screen reader.
- Text contrast meets WCAG 2.1 AA.
- Confidence, score levels and tags are shown as text as well as colour.
- Scenario and result text is written at a reading level suitable for professional adults.
- Quotations are shown in a distinct style and identified as the learner's own words.

---

## 8. Workflow

The end-to-end workflow, the role swimlanes, the decision points and the key journeys are in the Workflow folder: `../Workflow/Workflow.md`.
