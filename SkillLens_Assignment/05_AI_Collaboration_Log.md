# AI Collaboration Log

This log records how AI tools were used in preparing this submission, where they helped, where they were wrong or weak, and what decisions were made by the author.

---

## 1. Tools Used

| Tool | Used for |
|---|---|
| Claude (Anthropic) | Framing the problem, drafting and revising the PRD, metrics and roadmap, checking requirements against the course packet, research on public sources, and formatting |
| Claude Code (terminal) | Creating the folder structure, editing and reorganising Markdown files, and extracting text from the course packet |
| Figma (AI design features) | First-pass wireframes for screens S0 to S6 |
| Cursor chat in Figma | Generating and refining wireframe layouts from written prompts (see section 4) |

---

## 2. Where AI Helped

- **Discovery:** searched public sources on Skillsoft's Skill Benchmark Assessments, Percipio, and published work on LLM-based scoring reliability.
- **Drafting:** first-pass structure for the PRD, the metrics appendix, the roadmap and the UX specification.
- **Prioritisation:** proposed a feature table and a set of MVP cut lines, which were then reviewed and changed.
- **Metrics:** proposed a measurement framework (agreement, verifiability, consistency, routing recall, bias and gaming checks), which was then refined.
- **Risk review:** listed product risks and controls, including bias, misquoted evidence and over-reliance.
- **Wireframing:** first-pass screen layouts in Figma, from written screen specifications.
- **Risk and economics notes:** first drafts of the risk register, harm scenarios and the cost model. Every cost input is labelled as an assumption.
- **Consistency checks:** comparing documents against the course packet's required sections and checklist.

---

## 3. Where AI Was Weak or Wrong

| Issue | What happened | How it was handled |
|---|---|---|
| Generic outputs | The first draft was written in general product-management language and did not name a specific learner, workflow or decision | Narrowed to a specific decision (which applied abilities a learner lacks) and a defined first wedge (Python for data analysis) |
| Unsupported thresholds | Early drafts proposed numeric targets (for example, QWK ≥ 0.70, within-one-level agreement ≥ 85%) without a source for each | Kept as proposals, with the basis stated. The 0.70 reliability threshold was confirmed by the author as correct |
| Illustrative prices | The economics note needs model prices, which were not available from a live source | Labelled as illustrative assumptions, with a check against current provider pricing before any pricing decision |
| Secondary figures | A growth figure (994%) and a range of LLM–human agreement (0.30 to 0.80) came from secondary summaries rather than the original documents | Flagged in the PRD as company-reported or secondary. Originals to be checked before citation |
| Self-reported confidence | The first draft asked the model to report its own confidence | Removed. Confidence is determined by code, from three scoring runs and a quotation check |
| Inconsistent scope | Drafts mixed "individual" and "team" submission, and mixed the approved hiring and business tracks with the narrowed scope | Corrected to an individual submission, with hiring and business tracks placed after the MVP |
| Stale content | Lesson-recommendation language remained in the UX specification after the product direction changed | Replaced with feedback and follow-up scenarios, and a new screen (S6) added |
| Visual output | Figma-generated screens used colour and a styled look, not the low-fidelity wireframes asked for | Coloured screens kept for the submission, as the author's decision |
| Format assumptions | Early wireframes were written as text blocks, which are not wireframes | Replaced with a written specification, and visual wireframes produced in Figma |

---

## 4. Wireframes

### 4.1 Process

1. The screen specification was written first, using the screen inventory and the requirements in the PRD.
2. A global style prompt was entered in Cursor chat in Figma, followed by one prompt per screen, to generate a first-pass layout.
3. Each generated screen was checked against the specification. Labels were corrected where the AI rewrote them.
4. The resulting frames were exported as PNG files and embedded in the UX specification (`Appendix/Wireframes/UX_and_Workflow_Specification.md`).

### 4.2 Prompts used

**Global style prompt (entered first)**

```
Low-fidelity wireframes for SkillLens, a web app where learners practise applied skills. Grayscale only: no brand colours, no illustrations, no images, no icons other than simple check marks. Use plain rectangles for buttons, text fields and tables. Use clear, plain-language English labels exactly as written in each request. Include a footer line on every learner screen: "Development guidance, not a performance rating."
```

**S0: Skill selection (mobile, 390×844)**

```
Mobile screen, 390×844. Top bar with the product name "SkillLens". Heading: "Choose a skill to practise". Two selectable cards, each with a radio button:
- "Python for data analysis", subtitle "6 scenarios"
- "Communication skills", subtitle "2 scenarios"
Below them an optional text field labelled "Your most recent benchmark score (optional)". Primary button at the bottom: "Continue". Footer line: "Development guidance, not a performance rating."
```

**S1: Scenario and response (mobile, 390×844)**

```
Mobile screen, 390×844. Top bar: "Python for data analysis · Scenario 2 of 6". A scenario text block of about eight lines of placeholder text. A panel titled "You will be assessed on" listing four items: "Load and validate data", "Handle missing and inconsistent values", "Aggregate correctly", "Interpret and qualify results". A large multi-line text area labelled "Your response", with "Words: 0" at its bottom right. Helper text under it: "Explain your reasoning and the steps you would take." Primary button "Submit" at the bottom, with a second version of it greyed out to show the disabled state. Footer line.
```

**S2: Results and feedback (mobile, 390×844, scrolling)**

```
Mobile screen, 390×844, scrollable. Heading: "Your results". A chip reading "Confidence: High". An overall label reading "Developing". Four objective cards, stacked. Each card has:
- Objective name, for example "Load and validate data"
- "Score 2 of 3"
- A quote box titled "From your response" containing one short example quotation
- A line titled "To reach the next level" with one sentence of feedback
Cards with a score below 3 show a button "Practise this objective". At the bottom: a secondary button "Request review". Footer line.
```

**S3: Pending review (mobile, 390×844)**

```
Mobile screen, 390×844. Heading: "A reviewer will confirm this result." Body text: "No score is shown until a reviewer has checked it. Your response has been saved." A status tag reading "Pending review" with a sample date and time. Two buttons at the bottom: "Back to skills" (secondary) and "Try another scenario" (primary). No scores, no objective breakdown on this screen. Footer line.
```

**S4: Reviewer (desktop, 1440×900)**

```
Desktop screen, 1440×900. Two columns. Left column titled "Learner response": a long text block with two highlighted quoted spans. Right column titled "AI scoring": a table with four rows for the objectives, and columns "Score", "Quote", "Verified" (check mark) and "Runs agreeing" (for example "2 of 3"). Under the table, a decision block for each objective with two options, "Confirm" and "Override". When "Override" is selected, show a number field for a new score from 0 to 3. Below that, a required text area labelled "Reason for override". A status indicator reading "Pending", "Confirmed" or "Overridden". Buttons: "Save decision" (primary) and "Cancel" (secondary).
```

**S5: Reviewed result (mobile, 390×844)**

```
Mobile screen, 390×844. Same layout as the results screen. Add a status line at the top: "Reviewed on 12 March 2026 by reviewer. Scores: confirmed." Show two objective cards with scores and feedback. A collapsed row titled "Reviewer note" that can be opened. Footer line.
```

**S6: Follow-up result with score change (mobile, 390×844)**

```
Mobile screen, 390×844. Heading: "Objective: Handle missing and inconsistent values". Two rows, one above the other: "First attempt: 1 of 3" and "Follow-up: 2 of 3". Between them, a change indicator reading "Up 1 level". Below, a quote box with the follow-up quotation and one line of feedback. Two buttons at the bottom: "Practise another objective" (secondary) and "Done" (primary). Footer line.
```

### 4.3 Where the AI was weak in the wireframes

- Labels were rewritten by the tool in some screens and had to be corrected to match the specification.
- Layouts were styled, with colour and rounded elements, despite the grayscale instruction.
- Each regeneration produced different layouts, so the author selected the version that matched the specification best.

---

## 5. Human Corrections and Decisions

| Area | AI suggestion | Decision by the author | Reason |
|---|---|---|---|
| Submission type | Team-style language | Individual submission | Confirmed as allowed for this course |
| Scope | Broad, including hiring and business tracks | Skill-agnostic product; Python for data analysis as the worked example; hiring and business tracks after the MVP | Keeps the MVP narrow enough to test |
| Second skill | Not specified | Communication skills, with two scenarios | Open-ended responses suit communication, and it tests the skill-agnostic design |
| Confidence | Model reports its own confidence | Confidence determined by code from three runs and a quotation check | Self-reported confidence is poorly calibrated |
| Benchmark items | Mapped to objectives, graded automatically | Not used in scoring in the MVP | The benchmark items are multiple-choice and matching; the MVP scores open-ended responses |
| Remediation | Lesson recommendations | Rubric-based feedback and follow-up scenarios on the same objective | Keeps the AI central to the product and measurable |
| Micro-courses | Proposed as the remediation delivery | Moved to a post-MVP option | Production effort and dependency on item-level data would delay the core test |
| Thresholds | Numeric targets proposed by the AI | Kept as proposals, to be validated on the reference set before release | Targets must be tested, not assumed |
| Skillsoft role | Build a standalone learning platform | Skillsoft provides the catalogue, learner platform and delivery; SkillLens builds open-ended assessment, rubric scoring, and feedback | The catalogue already exists; the gap is open-ended, evidence-based assessment |

---

## 6. Final Reflection

- **Where AI accelerated the work:** research on public sources, first-pass drafting of long documents, consistency checks against the course packet, and first-pass wireframes. These saved a large amount of time.
- **Where AI could not replace product reasoning:** choosing the scope, deciding what the AI should and should not do, accepting risks, setting thresholds, and deciding that the product should not depend on benchmark item data. These decisions were made by the author and are recorded in section 5.
- **What needs checking before submission:** the 994% figure is company-reported and must be cited as such. The LLM agreement range (0.30 to 0.80) comes from a secondary synthesis and should be cited as such. The wireframes are kept in colour, as the author's decision.
