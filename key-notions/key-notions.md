# Key Notions

The following list identifies the key notions of KGRAIN, which need to be represented by the knowledge graph in order to answer the [competency questions](../competency-questions/competency-questions.md)(CQs). 

As running examples, we will consider two professions: **software developer** and **physician**. They belong to very different fields, and both have open question datasets. There are common skills like communication in both professions.

The notions are listed in the order they first appear in the CQs. Source datasets are optional for this project and are filled in where an existing dataset fits

## Interview Setup

* **Session**
    * Rationale: One interview from setup to stop
    * Connected Pattern: Event
    * Source Dataset(s): Synthetic sessions

* **InterviewType**
    * Rationale: Technical, Behavioral or HR. It classifies each question, and decides which selection rules a session uses, and holds the weak and strong thresholds for bands.
    * Connected Pattern: Explicit Typing
    * Source Dataset(s):

* **DifficultyLevel**
    * Rationale: Easy, Medium or Hard. The level a session is set to, and the level of a question.
    * Connected Pattern: Explicit Typing
    * Source Dataset(s):

* **Length**
    * Rationale: How long the session is set to run, in minutes.
    * Connected Pattern: Quantity
    * Source Dataset(s): Synthetic sessions

* **CandidateRole**
    * Rationale: The role of the person being interviewed in one session.
    * Connected Pattern: AgentRole
    * Source Dataset(s): Synthetic sessions

* **Person**
    * Rationale: The human who plays the candidate role.
    * Connected Pattern: AgentRole
    * Source Dataset(s): Synthetic sessions

* **JobDescription**
    * Rationale: document that provides information regarding the job description and its requirements. It determines the skills of the session and the occupation of the interview.
    * Connected Pattern: 
    * Source Dataset(s):

* **CV**
    * Rationale: Candidate’s CV. The skills listed get a CV raise in beginning. The listing only serves as evidence and not proof of the skill.
    * Connected Pattern:
    * Source Dataset(s): Resume Dataset

* **Skill**
    * Rationale: An ability or area of knowledge that interview questions can assess.
    * Connected Pattern: 
    * Source Dataset(s):

* **SkillRequirement**
    * Rationale: One skill required by one job description.
    * Connected Pattern:
    * Source Dataset(s):

* **ImportanceRating**
    * Rationale: How important a required skill is to the job, from 1 (least) to 5 (most).
    * Connected Pattern:
    * Source Dataset(s):

* **SkillEstimate**
    * Rationale: The system's estimate of the candidate's level in one skill in one session.
    * Connected Pattern: Observation
    * Source Dataset(s):

* **BaseLevel**
    * Rationale: The initial value that is assigned to each evaluated skill by a session’s selected difficulty level. 
    * Connected Pattern:
    * Source Dataset(s):

## Job Description, Profession & CV

* **Profession**
    * Rationale: A recognised type of work, such as software developer or physician.
    * Connected Pattern:
    * Source Dataset(s):

* **Field**
    * Rationale: A broad area of work, such as software or medicine, in which professions and field-specific skills are grouped. A profession can belong to more than one field.
    * Connected Pattern:
    * Source Dataset(s):

* **QuestionBank**
    * Rationale: All the questions the system can choose from. The selection rules only pick from the bank.
    * Connected Pattern: Part-Whole
    * Source Dataset(s):

* **Question**
    * Rationale: One item in the bank. Each question tests one or more skills, has an interview type, a difficulty level, expected minutes and a rubric.
    * Connected Pattern:
    * Source Dataset(s):

## Skills and how they relate

* **Prerequisite**
    * Rationale: A skill that should be learned before another, such as function calls before recursion. After a weak answer, the session can step back to it.
    * Connected Pattern: 
    * Source Dataset(s):

* **Subskill**
    * Rationale: A skill which is smaller and a subset of a larger skill, for instance, Joins in SQL. This is not the same type of relationship as Prerequisite; testing subskill will not test the entire skill.
    * Connected Pattern: Part-Whole
    * Source Dataset(s):

* **SkillType**
    * Rationale: Whether a skill is field-specific (recursion, reading an ECG) or general (communication, teamwork). General skills are what make cross-field questions possible.
    * Connected Pattern:
    * Source Dataset(s):

## Question Bank

* **MainSkill**
    * Rationale: The single skill a question focuses on. The responses to answers (easy question, hard question, prerequisite check) apply to it. This is definitely one of the skills a question tests.
    * Connected Pattern: 
    * Source Dataset(s):

* **OpeningQuestion**
    * Rationale: A warm-up question such as "Tell me about yourself". It tests no skill, has no interview type, and is picked only at turn 1.
    * Connected Pattern:
    * Source Dataset(s):

* **DifficultyScore**
    * Rationale: A number on each technical question, on the same scale as skill estimates, so questions can be matched to the candidate's estimated level and ranked as easier or harder.
    * Connected Pattern: Quantity
    * Source Dataset(s):

* **CutPoint**
    * Rationale: The two difficulty scores that turn a technical question's score into Easy, Medium or Hard (below the lower is Easy, from the lower up to the upper is Medium, from the upper up is Hard).
    * Connected Pattern: Quantity
    * Source Dataset(s):

* **ExpectedMinutes**
    * Rationale: Time required for asking and answering a question. It is used only for checking if the question can fit within the time available.
    * Connected Pattern: Quantity
    * Source Dataset(s):

* **Rubric**
    * Rationale: A set of weighted criteria used to score answers.
    * Connected Pattern: Part-Whole
    * Source Dataset(s):

* **FollowUp**
    * Rationale: This is a follow-up question that may be asked on a particular rubric criterion. This follow-up question is based on a good answer or low criterion score.
    * Connected Pattern:
    * Source Dataset(s):

* **Criterion**
    * Rationale: An aspect that is being evaluated in an answer, for instance correctness, clarity or results. This criterion may be used in more than one rubric.
    * Connected Pattern: 
    * Source Dataset(s):

* **RubricCriterion**
    * Rationale: The use of one criterion in one rubric, with the weight it has there.
    * Connected Pattern: 
    * Source Dataset(s):

* **Weight**
    * Rationale: How much a criterion counts in one rubric, from 0 to 1.
    * Connected Pattern:
    * Source Dataset(s):


## The interview so far

* **Turn**
    * Rationale: One question asked in a session, with its turn number and its answer.
    * Connected Pattern: Sequence, Event
    * Source Dataset(s): Synthetic sessions

* **Answer**
    * Rationale: What the candidate said at a turn. The selection rules react to how it was scored.
    * Connected Pattern: Observation
    * Source Dataset(s):

* **Score**
    * Rationale: An answer's overall score, from 0 to 1. Compared with the thresholds, it gives the band.
    * Connected Pattern: Observation
    * Source Dataset(s):

* **CorrectnessLabel**
    * Rationale: Accuracy of the core of an answer (Correct, PartlyCorrect, Incorrect). It does not depend on the score: even a correct answer may be scored low for clarity.
    * Connected Pattern: 
    * Source Dataset(s):

* **CriterionScore**
    * Rationale: An answer's score on one criterion, from 0 to 1.
    * Connected Pattern:
    * Source Dataset(s):

* **StartTime**
    * Rationale: When the session began. Minutes passes and remaining are calculated based on it and the length.
    * Connected Pattern:
    * Source Dataset(s):

## Choosing the next question

* **Band**
    * Rationale: Weak, Acceptable or Strong, given to an answer by comparing its score with the interview type's thresholds.
    * Connected Pattern: 
    * Source Dataset(s):

* **Threshold**
    * Rationale: A score boundary. The weak and strong thresholds of an interview type turn an answer's score into a band.
    * Connected Pattern: Quantity
    * Source Dataset(s):

* **RulePosition**
    * Rationale: Where a rule sits in the order used by one interview type.
    * Connected Pattern: Sequence
    * Source Dataset(s):

* **SelectionRule**
    * Rationale: A general rule for picking the next question: opening, easier question, prerequisite check, follow-up, harder question, criterion follow-up, new skill or revisit. These rules are what make the interview adaptive.
    * Connected Pattern: Explicit Typing
    * Source Dataset(s):

* **SelectionDecision**
    * Rationale: The record of why a turn's question was picked: the rule used, the answer that triggered it (if any), the higher rules that could not pick a question, and the estimates used.
    * Connected Pattern:
    * Source Dataset(s):

* **StopReason**
    * Rationale: Why a session ended: time up, no available question left, or no rule can pick a question.
    * Connected Pattern:
    * Source Dataset(s):

## Estimated Skill Level

* **StartingEstimate**
    * Rationale: The first estimate of a skill in a session, created when the skill becomes evaluated.
    * Connected Pattern:
    * Source Dataset(s):

* **CVRaise**
    * Rationale: A fixed amount added to the starting level of a skill the CV mentions.
    * Connected Pattern: Quantity
    * Source Dataset(s):

* **StandardError**
    * Rationale: How uncertain an estimate is; smaller means more precise.
    * Connected Pattern:
    * Source Dataset(s):

