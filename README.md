# KGRAIN: A Knowledge Graph for Reasoning in Adaptive Interviews

KGRAIN is an ontology and knowledge graph for adaptive interviews in which the next question depends on the performance of the candidate on earlier questions.

Good interviewers always know how to adapt. If the candidate fails to provide a satisfactory answer, then they proceed with a simpler question or try the prerequisite skill for it. If the candidate performs well, then he or she goes further into probing his or her answers. It is also important that all the skills required for the job are examined. KGRAIN stores all this logic in a graph form.

It is not limited to a particular career field or application. The same ontology can be used for any individual irrespective of the profession that he or she belongs to, whether it is a software engineer, an accountant, or a physician. And for any system that runs interviews on its own.

## The idea in short

* Questions are selected from the question bank. A question has difficulty and is associated with certain skills.
* Job description specifies relevant skills and their importance. CV, if provided, helps identify initial knowledge about relevant skills.
* Following each response, a small list of ordered rules is applied to determine what is the next question: an easier question, its prerequisite, follow-up, harder question, a new skill or skill requiring additional verification.
* Technical interviews adopt two concepts of CAT: each question has a difficulty level, each skill has an estimated level updated after each response.

## What's here

| Folder | Contents |
|---|---|
| [competency-questions](competency-questions/competency-questions.md) | The questions our knowledge graph should be able to answer, with how the next question is picked and the key terms |

The ontology, schema diagrams and example data will be added as the project goes on.

---
Course project for CS 7810: Introduction to Knowledge Engineering, Wright State University.

---
**Authors:** Diwakar Dahal, Awatar Gautam
