# SkillLens: Workflow

This document describes how work moves through SkillLens: who acts at each step, what the system decides, and what each role sees. The swimlane diagram in this folder (`Swimlane_Workflow.svg`) shows the same flow by role. The wireframes and screen behaviour are in the UX specification (`../Wireframes/UX_and_Workflow_Specification.md`).

The roles are the content owner (subject-matter expert), the learner, the SkillLens system, the AI model, the reviewer, and the integration partner.

---

## 1. End-to-End Flow

| Stage | Lane | Action | Output |
|---|---|---|---|
| 1. Author | Content owner | Writes scenarios, objectives and rubric level descriptors for a skill area | Draft skill area |
| 2. Test | Content owner | Builds a reference set of 40 responses, graded by two people, and runs the reliability tests | Reliability results |
| 3. Release | Content owner | Releases the skill area once every threshold is met | Live skill area |
| 4. Launch | Integration partner | Launches the assessment in its platform, through the API or an embedded widget | Learner access |
| 5. Browse | Learner | Opens the skill area and starts a scenario | Scenario opened |
| 6. Respond | Learner | Writes and submits a response | Submitted response |
| 7. Check | System | Confirms the response has at least 40 words and is on topic | Accepted or returned for revision |
| 8. Score | AI model | Scores each objective from 0 to 3, with a quotation, in three runs | Three sets of scores |
| 9. Verify | System | Checks every quotation against the response and sets confidence | High, medium or low confidence |
| 10. Show or hold | System | Shows high and medium results with feedback; holds low results for review | Learner view or review queue |
| 11. Review | Reviewer | Confirms or overrides each score, with a reason, and may add a comment | Decision and comment |
| 12. Practise | Learner | Chooses an objective below 3 and takes a follow-up scenario on it | Follow-up attempt |
| 13. Update | System | Calculates scenario score, skill proficiency and score change | Updated results |
| 14. Report | System | Builds scenario, skill and learner reports | Reports |
| 15. Export | Integration partner | Downloads CSV or receives JSON through the API | Data in the partner's systems |

---

## 2. Decision Points

| Decision | Made by | Rule | If yes | If no |
|---|---|---|---|---|
| Response long enough and on topic? | System | At least 40 words; at least one objective matched | Go to scoring | Learner is asked to expand or revise; no scoring |
| Quotations verified? | System | Every quotation appears in the response | Continue | Hold the result for review |
| Runs agree? | System | The three runs agree within one level on every objective | High confidence | Medium, or low if two or more levels differ |
| Confidence high or medium? | System | Result from the previous decision | Show the result to the learner | Hold the result for review |
| Reviewer overrides a score? | Reviewer | Reviewer judges the response differently | Score changes; reason recorded | Score confirmed |
| Learner practises an objective? | Learner | Objective scored below 3 | Follow-up scenario on that objective | No follow-up needed |

---

## 3. States of an Attempt

| State | Meaning | What the learner sees |
|---|---|---|
| Not submitted | Draft in progress | The response area |
| Returned | Response too short or off topic | A prompt to expand or revise |
| Scored | Scores and quotations produced | Results (after the checks) |
| Held | Waiting for a reviewer | Pending review |
| Confirmed | Reviewer confirmed all scores | Reviewed result |
| Overridden | Reviewer changed at least one score | Reviewed result with the reviewer's reason summarised |

A held attempt is never shown to the learner as a score until it is confirmed or overridden.

---

## 4. Role Responsibilities

**Content owner.** Owns the scenarios, objectives and rubrics for a skill area. Runs the reliability tests and releases the skill area. Reviews any AI-assisted drafting before release. Coming-soon authoring will bring AI-assisted drafting into this lane.

**Learner.** Browses skill areas, starts scenarios, writes responses, reads results, and practises weak objectives. Sees only their own results and the reviewer comments on them.

**System.** Applies the rules in section 2, keeps the audit record, calculates scenario scores and skill proficiency, and builds the reports and exports. It never decides a score by itself; the AI model scores and the system checks.

**AI model.** Scores each objective from 0 to 3 against the rubric, with a verbatim quotation for each score above 0. It does not report its own confidence and does not write feedback for the learner.

**Reviewer.** Works the review queue. Confirms or overrides each held score, with a reason for any override. May add a comment for the learner. Cannot edit the learner's response.

**Integration partner.** Launches the assessment, receives results through the API or downloads them as CSV, and uses the reports in its own platform. It is responsible for its learners' data under the agreement.

---

## 5. Key Journeys

**Journey A: practise and improve.** The learner opens a skill area, starts a scenario, submits a response, sees the scenario score and feedback, practises one objective, and sees the score change.

**Journey B: held result.** The learner submits a response that is held. A reviewer confirms or overrides it and may add a comment. The learner sees the reviewed result and the comment.

**Journey C: reporting and export.** A reviewer or partner opens the scenario and skill report, filters to one skill area, and exports the data as CSV or JSON. The same values appear in both formats.

---

## 6. Coming-Soon Paths

- **Docker, Product management and Leadership:** shown as coming soon. No content, no start action and no accordion. They enter the workflow only when released through the content owner's release step.
- **Authoring:** shown in the reviewer area as coming soon. When released, the content owner's steps 1 and 2 will be supported by AI-assisted drafting, with human review before release.
