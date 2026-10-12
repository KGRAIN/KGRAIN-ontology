# Competency Questions

**KGRAIN: A Knowledge Graph for Reasoning in Adaptive Interviews**

## Purpose

KGRAIN is a knowledge graph for adaptive interviews, where each question depends on how the candidate answered the earlier ones. A good interviewer does this naturally. They open with a warm-up question to put the candidate at ease. After a weak answer they ask something easier or check a skill that should have come first. After a strong answer they go deeper. They make sure every skill the job needs gets asked about, and if there is time left, they use it to get a better picture of the candidate. We want the graph to hold this reasoning, so that both the next question and the reason it was chosen can be read from the graph.

KGRAIN is meant for any system that runs an interview on its own: it picks each question and gets a score for each answer. It does not depend on any particular application. Before an interview starts, the system needs:

1. **Documents:** a job description (required) and a CV (optional).
2. **Settings:** interview type (Technical, Behavioral or HR), difficulty (Easy, Medium or Hard) and length in minutes.

The graph should work for any job, for example a software developer, a chartered accountant or a physician.

Two ideas come from computerized adaptive testing (CAT). Each technical question has a *difficulty score*, and the candidate has an *estimated skill level* for each skill, which changes after every answer.

## Interview setup

| # | Competency question | Expected answer |
|---|---|---|
| 1 ★ | What interview type, difficulty level and length was `Session` set up with? | One type, one difficulty level, a number of minutes |
| 2 | Who is the candidate in `Session`? | One person |
| 3 ★ | Which job description and CV does `Session` use? | One job description and at most one CV |
| 4 ★ | Which skills does the job description used in `Session` require? | A list of skills |
| 5 | Which interview types use estimated skill levels? | A list of interview types |
| 6 | What base level does difficulty level `Difficulty` set? | One number, the same for every skill |

## Job description, profession and CV

| # | Competency question | Expected answer |
|---|---|---|
| 7 | Which profession is `JobDesc` for? | One profession |
| 8 | Which fields is `Profession` associated with? | One or more fields |
| 9 ★ | Which skills does `JobDesc` rate as most important, and what are their ratings? | One or more skills, each with its rating |
| 10 | What is the importance rating of `Skill` in `JobDesc`? | A number from 1 to 5, or none if `JobDesc` does not require `Skill` |
| 11 ★ | Which skills required by the job description in `Session` are mentioned in the CV used in `Session`? | A list of skills; empty if there is no CV |
| 12 ★ | Which skills required by the job description in `Session` have no question of the chosen interview type in the question bank? | A list of skills; empty if every required skill has at least one |

## Skills and how they relate

| # | Competency question | Expected answer |
|---|---|---|
| 13 | Which skills must be learned directly before `Skill`? | A list of skills |
| 14 ★ | Which skills must be learned before `Skill`, directly or indirectly? | A list of skills |
| 15 | Which skills have `Skill` as a direct prerequisite? | A list of skills |
| 16 | Which subskills directly make up `Skill`? | A list of skills |
| 17 | Is `Skill` field-specific or general? | Field-specific or general |
| 18 | Which field does the field-specific skill `Skill` belong to? | One field |

## Question bank

| # | Competency question | Expected answer |
|---|---|---|
| 19 ★ | Which skills does `Question` test, and which one is its main skill? | One or more skills, and one main skill among them; none for an opening question |
| 20 | Which interview type is `Question` for? | One interview type, or every type for an opening question |
| 21 | What is the difficulty score of `Question`? | One number, for technical questions only |
| 22 | What difficulty level does `Question` have? | Easy, Medium or Hard |
| 23 | How many minutes is `Question` expected to take? | One number |
| 24 | Which rubric is used to score answers to `Question`? | One rubric |
| 25 | Which questions test `Skill` at difficulty level `Difficulty`? | A list of questions; an empty list shows a gap in the question bank |
| 26 ★ | Which technical question on `Skill` has the highest difficulty score? | One or more questions; none if `Skill` has no technical questions |
| 27 | Which follow-up questions belong to `Question`? | A list of questions |
| 28 | Which rubric criterion does `FollowUp` ask about? | One criterion, or none |
| 29 | Which criterion or criteria have the highest weight in `Rubric`? | One or more criteria |
| 30 | What is the weight of `Criterion` in its rubric? | A number between 0 and 1 |
| 31 | Which questions in the question bank are opening questions? | A list of questions; empty means no interview can open with a warm-up |

## The interview so far

| # | Competency question | Expected answer |
|---|---|---|
| 32 ★ | Which question was asked at turn `n` of `Session`? | One question |
| 33 | How many questions have been answered in `Session`? | One number |
| 34 | What score did the answer at turn `n` of `Session` get? | A number between 0 and 1 |
| 35 | Was the answer at turn `n` of `Session` marked correct, partly correct or incorrect? | One of the three labels |
| 36 ★ | On which rubric criterion or criteria did the answer at turn `n` of `Session` score lowest, and what were the scores? | One or more criteria, with their scores |
| 37 | What score did the answer at turn `n` of `Session` get on `Criterion`? | A number between 0 and 1 |
| 38 ★ | Which testable required skills has `Session` not covered yet, from highest to lowest importance rating? | An ordered list of skills; skills with the same rating can be in any order |
| 39 | How many minutes have passed in `Session` so far? | One number |
| 40 ★ | How many minutes are left in `Session`? | One number: the set length minus the minutes passed, never below 0 |

## Choosing the next question

| # | Competency question | Expected answer |
|---|---|---|
| 41 ★ | What band, if any, did the latest answer in `Session` get? | Weak, acceptable or strong; none if there is no answer yet, the latest answer is to an opening question, or the interview type has no bands |
| 42 | What are the weak and strong score thresholds for `Type`? | Two numbers, or none if the type has no bands |
| 43 ★ | For `Type`, which rule comes first after an answer in `Band`? | One rule; none if the type has no bands |
| 44 | For `Type`, which rule applies after an answer with a low criterion score? | One rule; none if the type has no such rule |
| 45 | Which rules does `Type` use, in order? | An ordered list of rules |
| 46 ★ | If `Session` should not stop, which question comes next, and which rule picked it? | One question and one rule (see [How the next question is chosen](#how-the-next-question-is-chosen)); none if `Session` should stop (question 55) or no rule can pick an available question |
| 47 | Which unasked questions of the chosen interview type in `Session` are expected to take longer than the minutes left? | A list of questions |
| 48 | After a weak answer to the technical question `Question`, which available technical questions on the same skill have a lower difficulty score and are closest in score to `Question`? | One or more questions; none if no such question is available |
| 49 ★ | After a weak answer on `Skill`, which direct prerequisites of `Skill` are not covered yet in `Session` and have an available question? | A list of skills |
| 50 | After a weak answer on `Skill`, which direct prerequisites of `Skill` are not covered yet in `Session` but have no available question? | A list of skills. Nothing can be asked about these, so the next rule is tried |
| 51 | Which available technical question on `Skill` has the lowest difficulty score? | One or more questions; none if no technical question on `Skill` is available, even if Behavioral or HR ones are |
| 52 | After a strong answer to the technical question `Question`, which available technical questions on the same skill have a higher difficulty score and are closest in score to `Question`? | One or more questions; none if no such question is available |
| 53 | After a low score on `Criterion` in the answer to `Question`, which available follow-ups of `Question` ask about `Criterion`? | A list of questions; empty if none is available |
| 54 | Which testable required skills that still have an available question have the fewest answered questions in `Session`? | A list of skills; empty if no testable required skill has an available question. The revisit rule picks from this list |
| 55 ★ | Should `Session` stop because time is up, no available questions are left, or no rule can pick an available question? | Yes or no, with the reason or reasons. Covering every testable required skill does not stop the session |

## Estimated skill level

Only Technical interviews use estimated skill levels, so these questions return none for Behavioral and HR sessions.

| # | Competency question | Expected answer |
|---|---|---|
| 56 ★ | What is the starting level for `Skill` in `Session`, and how is it made up? | One number, split into base level and CV raise (0 if the CV does not mention the skill or there is no CV); none if `Skill` is not assessed in `Session` |
| 57 | How much is added to the base level for a skill mentioned in the CV? | One number |
| 58 | What is the current estimated skill level for `Skill` in `Session`? | One number; none if `Skill` is not assessed in `Session` |
| 59 | What was the estimated skill level for `Skill` in `Session` before its latest update? | One number, or none if it was never updated |
| 60 | Which answer caused the latest update to the estimate for `Skill` in `Session`? | One answer, or none if it was never updated |
| 61 | What is the standard error of the current estimate for `Skill` in `Session`? | One number; none if `Skill` is not assessed in `Session` |
| 62 ★ | Which available technical question on `Skill` best matches the candidate's current estimated level? | One or more questions; none if `Skill` is not assessed in `Session` or no such question is available |
| 63 | Which assessed skills in `Session` now have an estimate above their starting level? | A list of skills |
| 64 | Which skills had their estimates updated by the answer at turn `n` of `Session`? | A list of skills, one per updated estimate |

## Why a question was asked

| # | Competency question | Expected answer |
|---|---|---|
| 65 ★ | Which rule picked the question at turn `n` of `Session`, and what made that rule apply? | One rule and its condition (for example, a weak band on the previous answer); at turn 1, the opening rule, or the new-skill rule if no opening question is available |
| 66 | Which rules ranked above the one that picked the question at turn `n` of `Session` applied but had no available question? | A list of rules; empty if there were none |
| 67 ★ | When the question at turn `n` of `Session` was picked, what was the estimated level of each skill it tests? | One estimate per skill, as it was at that moment; none for Behavioral and HR sessions and for an opening question |

## Feedback to the candidate

| # | Competency question | Expected answer |
|---|---|---|
| 68 ★ | Of the required skills covered in `Session`, which have the lowest current estimated level? | One or more skills; none if the session is Behavioral or HR, or no required skill is covered yet |
| 69 | Across all answers in `Session`, which rubric criterion has the lowest average score? | One or more criteria, each with its average and the number of answers it is based on; none if no criterion was scored |

## Working across fields

| # | Competency question | Expected answer |
|---|---|---|
| 70 ★ | Which skills are required in more than one field? | A list of skills; empty if there are none |
| 71 | Which professions have at least one job description that requires `Skill`? | A list of professions; empty if no job description requires it |
| 72 | Which rubrics are used by questions from more than one field? | A list of rubrics, counting the fields of every question that uses each rubric; empty if there are none |
| 73 ★ | Does `Question` test only general skills? | Yes or no |

## Consistency checks

These questions check that the data agrees with itself. Questions 74, 75, 77 and 78 should find no problems. Question 76 is different: it only points out answers that are worth a second look.

| # | Competency question | Expected answer |
|---|---|---|
| 74 | Does every answer in `Session` that has an overall score or any criterion score have an overall score equal to the weighted sum of its criterion scores (within 0.01)? | Yes or no; a missing overall score or a missing criterion score counts as a mismatch |
| 75 | Does `Rubric` have at least one criterion, with weights that add up to 1? | Yes or no |
| 76 | Which technical answers are marked correct but scored weak, or marked incorrect but scored strong? | A list of answers to review for a possible scoring mistake; usually empty. Partly correct answers are not checked |
| 77 | Are the turns in `Session` numbered 1, 2, 3 and so on, in the order the questions were asked, with no repeats or gaps? | Yes or no |
| 78 | Which skills are their own prerequisite, directly or through a chain? | A list of skills; should be empty |
