# Competency Questions

**KGRAIN: A Knowledge Graph for Reasoning in Adaptive Interviews**

## Purpose

KGRAIN is a knowledge graph for adaptive interviews, where each question depends on how the candidate answered the earlier ones. A good interviewer does this naturally. They open with a warm-up question to put the candidate at ease. After a weak answer they ask something easier or check a skill that should have come first. After a strong answer they go deeper. They make sure every skill the job needs gets asked about, and if there is time left, they use it to get a better picture of the candidate. We want the graph to hold this reasoning, so that both the next question and the reason it was chosen can be read from the graph.

KGRAIN is meant for any system that runs an interview on its own: it picks each question and gets a score for each answer. It does not depend on any particular application. Before an interview starts, the system needs:

1. **Documents:** a job description (required) and a CV (optional).
2. **Settings:** interview type (Technical, Behavioral or HR), difficulty (Easy, Medium or Hard) and length in minutes.

The graph should work for any job, for example a software developer, a chartered accountant or a physician.

Two ideas come from computerized adaptive testing (CAT). Each technical question has a *difficulty score*, and the candidate has an *estimated skill level* for each skill, which changes after every answer.

## How to read the questions

* Names in `code` are placeholders for a specific item: `Session` (an interview), `n` (a turn number), `JobDesc` (a job description), `CV`, `Profession`, `Skill`, `Question`, `FollowUp` (a follow-up question), `Rubric`, `Criterion` (a rubric criterion), `Type` (an interview type), `Difficulty` (Easy, Medium or Hard) and `Band` (weak, acceptable or strong).
* The expected answer says what kind of answer comes back and how many.
* ★ marks our 25 core questions. The others add detail or check the data.
* Some words, like *covered* or *available*, have a fixed meaning. They are listed under [Key terms](#key-terms) at the end, and the way the next question is picked is explained in [How the next question is picked](#how-the-next-question-is-picked).


## Interview setup

| # | Competency question | Expected answer |
|---|---|---|
| 1 ★ | What interview type, difficulty level and length was `Session` set up with? | One type, one difficulty level, a number of minutes |
| 2 | Who is the candidate in `Session`? | One person |
| 3 ★ | Which job description and CV does `Session` use? | One job description and at most one CV |
| 4 ★ | Which skills does the job description in `Session` ask for, and how important is each one? | A list of skills, each with an importance rating from 1 to 5 |
| 5 | Which interview types use estimated skill levels? | A list of interview types |
| 6 | What base level does difficulty level `Difficulty` set? | One number, the same for every skill |

## Job description, profession and CV

| # | Competency question | Expected answer |
|---|---|---|
| 7 | Which profession is `JobDesc` for? | One profession |
| 8 | Which fields is `Profession` associated with? | One or more fields |
| 9 ★ | Which skills does `JobDesc` rate as most important, and what are their ratings? | One or more skills, each with its rating |
| 10 | How important is `Skill` in `JobDesc`? | A rating from 1 to 5, or none if `JobDesc` does not ask for `Skill` |
| 11 ★ | Which skills required by the job description in `Session` are mentioned in the CV used in `Session`? | A list of skills; empty if there is no CV |
| 11a | Which skills does `CV` mention? | A list of skills, including ones the job does not ask for. The starting level of any skill depends on this (question 56) |
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
| 41 ★ | Was the latest answer in `Session` weak, acceptable or strong? | One band; none if nothing has been answered yet, the latest answer was to an opening question, or the interview type has no bands |
| 42 | What are the weak and strong score thresholds for `Type`? | Two numbers, or none if the type has no bands |
| 43 ★ | For `Type`, which rule comes first after an answer in `Band`? | One rule; none if the type has no bands |
| 44 | For `Type`, which rule applies after an answer with a low criterion score? | One rule; none if the type has no such rule |
| 45 | Which rules does `Type` use, in order? | An ordered list of rules |
| 46 ★ | If `Session` is not over, which question comes next, and which rule picked it? | One question and one rule (see [How the next question is chosen](#how-the-next-question-is-chosen)); none if `Session` should stop (question 55) or no rule can pick an available question |
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


#    How the next question is chosen

Before each turn, the interview stops if time is up or there are no available questions left. Otherwise, the rules are tried in sequence, and the first successful rule will select the question. If none is successful, then the interview ends.

**The rules, in order:**

1. **Opening.** Turn 1 only. Warm-up question such as "Tell me about yourself." No skill is tested and it makes no difference to any estimate, and the following guidelines are ignorant to its answer.
2. **Rules that react to the last answer.**
   * **Technical**
        * after a weak answer: **easier question** (same main skill, lower difficulty) and **prerequisite check** (a direct prerequisite not covered yet).
        * after a strong answer: **follow-up** (a follow-up of the last question) and **harder question** (same main skill, higher difficulty).
   * **Behavioral and HR**
        * after a low criterion score: **criterion follow-up** (a follow-up about that criterion).
3. **New skill.** The most important required skill not covered yet.
4. **Revisit.** The required skill with the fewest answered questions so far. This is what keeps the interview going after every required skill has been covered.

The rule will consider only those criteria or skills that still have one or more questions. It will select among those choices in the following way:

| Rule | How it chooses |
|---|---|
| Easier / Harder Question | Next in terms of difficulty after the previous problem, and then next to its current estimate |
| Prerequisite Check | The prerequisite with the lowest estimate (or if it has not yet been estimated, its initial level of estimate), then its simplest available question |
| Follow-Up | Most similar in difficulty to the current estimate of the skill |
Criterion Follow-Up | The worst performing criterion that has a possible follow-up |
| New Skill | The most important skill, for technical questions, the one that is close in difficulty to this skill. For Behavioral and HR, the one of the same difficulty or closest level |
| Revisit | Fewest questions answered (a question is counted once for each of the skills it addresses), then most important, then chosen for a new skill 

In case any tie remains, the sequence of questions in the fixed question bank order resolves the issue, and the same circumstances lead to the same question each time. However, when answering the competency questions, the ties are preserved; "most," "lowest" or "closest" question returns all ties.

Just because all the skills have been asked about doesn’t mean the interview is finished. However, it’s important to note that an interview isn’t necessarily carried out until the time limit runs out – if there aren’t any more questions relating to any of the skills and no rules based on the previous answer can select another question, then it stops. That is on purpose, since the interview is about the skills the job asks for.

## Key terms

**Skills**

* **Skill:** test anything an interview can test. A *field-specific* skill is specific to that field only (recursion, tax accounting, ECG reading). A *general* skill is not (communication, teamwork).
* **Profession:** any kind of job, not only licensed professions.
* **Required skill:** skill listed on the job description of the session. The importance level is rated between 1 (the least) to 5 (the most). In case of a tie for the highest rating, they are all considered as “the most important.”
* **Testable required skill:** is one of the compulsory skills and will have at least one question from the interview section of the current session. It doesn’t mean that the questions are available right now, they may all have been asked or be too long.
* **Covered skill:** a skill that is tested through a question that has already been answered before. Testing a portion of a skill does not test the entire skill.
* **Prerequisite:** a skill that must be learned before another, such as function calls before recursion. **Prerequisites chain:** if variables appear before function calls, then they will appear before recursion.
* **Subskill:** a minor skill which is a subset of a major skill, for example, the joins in SQL. But this is not the same thing as a prerequisite since the function call comes before recursion but does not constitute it.
* **Required in a field:** a skill is necessary in a particular field if it is a requirement of any job specification for any job in the field.

**Questions**

* **Main Skill:** the one skill a question tests primarily. The rules reacting to the answer make use of the primary skill tested by the previous question. However, a answer does get updated for all the skills involved in the question.
* **Opening Question:** a warm-up question, marked as such in the bank. Applicable to all interviews, tests no skill. Scoring based on its rubric, yet not given a band and does not affect any estimate.
* **Field of a question:** fields of the field-related skills it tests. A question testing general skills has no field.
* **Difficulty score:** is a figure that applies to every technical question and is used to determine the difficulty of a question. It is measured using the same scale as skill ratings, hence they can be compared. The behavioral and HR questions have no difficulty score.
* **Difficulty Level:** Easy, Medium or Hard. In technical questions, it is based on the difficulty score, which has two cut-off points. For non-technical questions, the level is assigned directly.
* **Closest / Best Fit:** the lowest absolute difference between the difficulty score of a question and some other number on the same scale (difficulty score or its estimation).
* **Available question:** one that has not been asked in this session of the selected type of interview, and which should be answered within the time left. Opening questions are available prior to the first answer.

**Answers**

* **Score and criterion score:** the total score given to the answer and the scores for each criterion on the rubric, both ranging from 0 to 1.
* **Average criterion score:** Average of scores of criterion among the answers to the criterion in a session.
* **Band:** weak (below weak threshold), strong (at or above the strong threshold) and acceptable (between weak and strong thresholds). Only technical answers earn a band, and different thresholds are set for each type of interview
* **Low criterion score:** a criterion score below the threshold set by its rubric.
* **Correct, partly correct, incorrect:** a tag on each answer indicating whether the essence of the answer (the solution, fact, or example required) is correct. This is independent of the score; thus, a correct answer may receive a low score on other parameters such as clarity.
* **Latest answer:** the answer with the highest turn number.

**Time**

* **Minutes passed:** exact time that has passed since the beginning of the interview, measured in seconds with no rounding off whatsoever; thus, 1.5 minutes to go is never counted as 2.
* **Expected minutes:** how long each question takes. Used only to determine whether the question still is valid, never to calculate the time taken.

**Skill estimates (Technical only)**

* **Estimated level:** a value indicating the ability of the candidate with respect to a specific skill on the same scale as difficulty values. The difference between the estimate and the difficulty value is not a probability but simply ranks the items.
* **Assessed skill:** a skill for which the session keeps an estimate. Required skills will always be assessed right from the beginning. Any other skill (such as a prerequisite skill) will become an assessed skill if a question based on that skill is selected.
* **Starting level:** the base level determined by the difficulty of the session, plus a fixed CV raise if the skill is mentioned in the CV. This is applicable for all skills mentioned in the CV, regardless of whether or not they are required.
* **Update:** after each answer, every skill the question tests gets a new estimate, which replaces the old one (it may stay the same).
* **Standard error:** how unsure an estimate is. Smaller means more precise.