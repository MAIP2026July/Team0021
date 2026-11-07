# Prototype Screen Recording

This folder holds the screen recording of the SkillLens prototype (`SkillLens_Assignment/04_Prototype/index.html`). The recording has no audio narration. This readme explains what is shown in each section and the inputs used, so that each step can be followed without sound.

## Recording details

- **Product shown:** SkillLens prototype, opened as a local file in a web browser. No server, account or network connection is needed.
- **Audio:** none. The recording is silent.
- **Sections:** five, recorded separately. The browser was reloaded before each section, so each one starts from a clean state.
- **Inputs:** typed or pasted text, listed under "Inputs used" below. Each response was pasted, not typed, so the output matches the expected results.

## Section 1: Introduction

The introduction shows the prototype's header and its notice. The "What this prototype does not prove" panel was opened on screen, showing the limitations: scoring is scripted rather than produced by a live model, the three-run confidence rule is not implemented, the automatic low-confidence route is not triggered, two scenarios are included per skill, the content is synthetic, and the prototype is not connected to Skillsoft or learner data.

## Inputs used

**Input A: strong response.** Used in Section 3. Pasted into the scenario "Weekly churn export". Expected result: all four objectives score 3, confidence High, overall band "Secure", and no feedback or follow-up is offered.

```
I would load the three CSV files and check the dtype of each column, because the dates use two formats. I would convert them with to_datetime, then check for duplicated user_id rows and remove the extra copies. If a check fails, I would flag the rows and log the issue before analysis. For missing plan_type values I would use fillna with 'unknown' rather than drop them, since dropping rows would bias the churn rate and skew the result. To calculate the rate I would use groupby on plan_type and divide churned users by the total users in each group, then run a sanity check to confirm the total matches the cohort denominator. The result only covers the 30 days in the export, a limitation that means it cannot show why customers left, so I would report that uncertainty.
```

**Input B: medium response.** Used in Sections 2 and 4. Pasted into the scenario "Weekly churn export". Expected result: confidence Medium with the borderline banner. Objectives O1, O2 and O4 score 1, and O3 scores 2. "Practise this objective" appears for O1, O2 and O4.

```
I would load the three CSV files and check the data types. The dates have two formats, so I would convert them. For missing plan_type values I would fill them with a placeholder. I would group by plan and divide the churned users by the total users to get the rate. The result covers only the 30 days in the export, so I would also note that it is a limited window.
```

**Input C: short response.** Used in Section 3. Expected result: the message "Please expand your response to at least 40 words (currently 20)." Nothing is scored.

```
I would load the files, check the dates, fill the missing plans and calculate the churn rate by plan type.
```

**Input D: off-topic response.** Used in Section 3. Expected result: the message "The response does not address the scenario. Please revise your response." Nothing is scored.

```
My favourite food is pizza, and I enjoy travelling to the mountains on weekends with my family, our dog, and friends. We often cook long dinners, watch films, read novels, and go hiking when the weather is warm and bright every single year.
```

**Input E: follow-up response on O2.** Used in Section 2. Entered after Input B, using "Practise this objective" under "Handle missing and inconsistent values". Expected result: "First attempt: 1 of 3", "Follow-up: 3 of 3", and "Up 2 levels".

```
I would handle missing order amounts by checking how many rows are affected first. I would fill with the median if the values are skewed, or drop them if the count is small, because filling can introduce bias and changes the average. I would state the effect on the result in the report, since a different method could move the regional figure.
```

## What each section shows

**Section 2: medium result, practice and score change.** Input B is submitted. The borderline banner is shown, and the objective scores are displayed with their quotations. "Practise this objective" is clicked for O2, and Input E is submitted. The follow-up result shows the change in the score.

**Section 3: strong result and input validation.** Input A is submitted, showing high confidence, the overall band and no feedback. Input C then shows the 40-word message, and Input D shows the off-topic message.

**Section 4: reviewer loop.** Input B is submitted, and "Request review" is clicked. The pending screen is shown. The Reviewer view is opened, the item is reviewed, and the score for "Load and validate data" is overridden to 2 with the reason: "The response names the data type and date-format checks, which meets the level 2 descriptor." The decision is saved. The Learner view is opened, and "Check status" is clicked to show the reviewed result, with the status "Scores: adjusted by reviewer".

**Section 5: closing.** The limitations panel is shown again, and the Skillsoft integration is described in the PRD (section 4.6).

