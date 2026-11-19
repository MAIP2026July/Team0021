# AI Collaboration Log

This log records the AI tools used in preparing this submission, the main areas where they helped, where their output needed correction, and the decisions made by the author.

---

## 1. Tools Used

| Tool | Used for |
|---|---|
| Claude (Anthropic) | Drafting and editing documents, drafting scenario, objective and rubric content for review, writing the prototype code, and checking documents against the course packet |
| Claude Code (terminal) | Organising files and folders, generating the wireframe and diagram files, and extracting text from the course packet |
| Figma (AI design features) | First-pass wireframes in an earlier layout, which were later replaced |

---

## 2. Where AI Helped

- **Research:** public sources on skills assessment platforms and published work on LLM-based scoring reliability.
- **Drafting:** first versions of the PRD, metrics, roadmap, risk note, economics note, UX specification and workflow description.
- **Content:** draft scenarios, objectives and rubric descriptors for the three live skill areas. These drafts were not reviewed by a subject-matter expert.
- **Prototype:** code for the browser prototype, including its scripted scorer and reports.
- **Diagrams:** the swimlane diagram and the desktop wireframes, generated as SVG from written specifications.
- **Checks:** comparing the documents against the course packet's required sections.

---

## 3. Where AI Output Needed Correction

| Issue | How it was handled |
|---|---|
| Generic framing in early drafts | Narrowed to one decision and then to a generic assessment integration point |
| Confidence reported by the model | Replaced with confidence determined by the system from repeated runs and a quotation check |
| Lesson-based remediation | Replaced with rubric-based feedback and follow-up scenarios |
| A rubric that said bidirectional search works on weighted graphs | Corrected to breadth-first search for unweighted graphs and Dijkstra's algorithm or A* for weighted graphs |
| Mixed submission language ("individual" and "team") | Corrected to an individual submission |
| Model prices and cost inputs not available from a live source | Labelled as illustrative assumptions in the economics note |
| Unverified citations | Authors and titles checked; unverifiable authors removed |
| Early wireframes written as text | Replaced with written specifications and drawn wireframes |
| Figma AI output varied between runs | Replaced with SVG wireframes generated from the written specifications |

---

## 4. Decisions by the Author

| Area | Decision | Reason |
|---|---|---|
| Positioning | An assessment integration point for learning platforms and enterprises, rather than a learning platform | The scoring, review and reporting work is where the product differs; building content and distribution would compete with existing platforms |
| Skill areas | Three live skill areas, each with three scenarios, and three coming-soon areas | Gives a complete loop in each live area without over-building |
| Skill proficiency | Average of the latest scores for attempted scenarios only | Unattempted scenarios should not lower a score |
| Reviewer comments | Shown to learners | Gives the learner a reason for any change |
| Reports and export | Scenario, skill and learner reports, with CSV and JSON export | Partners need the same values in their own systems |
| Pricing | A price per scored attempt, with a platform fee | Ties the cost of AI to use |
| AI cost | Model calls paid by the product; reviews paid by the integration owner by default | Keeps the human decision inside the customer's process |
| Thresholds | Kept as targets to be tested on the reference sets before release | Targets must be tested, not assumed |
| Authoring | Shown as coming soon | The authoring workspace depends on the review workflow being proven first |

---

## 5. Final Reflection

AI reduced the time needed for research, drafting, diagrams and prototype code. The scope, the risk acceptance, the thresholds, the pricing and the recommendation were decided by the author. The scenario and rubric drafts still need subject-matter review before any release.

Two figures are cited with their status: the 994% growth figure is company-reported, and the agreement range for LLM graders (0.30 to 0.80) comes from a secondary synthesis.
