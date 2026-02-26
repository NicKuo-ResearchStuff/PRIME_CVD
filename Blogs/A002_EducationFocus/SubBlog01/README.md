# PRIME-CVD Data Asset 1:</br> Designing Socioeconomic Stratification Assignments</br> with a Clean CVD Cohort

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog03.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we show how PRIME-CVD Data Asset 1 can be used to design assessment-ready assignments and exam questions that test students’ ability to reason about socioeconomic structure, distributional plausibility, and modelling readiness in cardiovascular risk data.

This entry is written for educators: lecturers, course convenors, and tutors teaching postgraduate health science, medical informatics, or applied data science.

Rather than focusing on exploratory play, the emphasis here is on assessment design — specifically, how a clean, causal cohort enables markable, reproducible, and fair evaluation tasks.

A fully worked reference solution (code and canonical figure) is included in the same folder as this blog.

---

## Why Socioeconomic Stratification Matters in Assessment

In real cardiovascular epidemiology and health services research, analysts are expected to interrogate datasets before fitting models:

* Are socioeconomic gradients present where we expect them?
* Are rare conditions truly rare, or artefacts of data processing?
* Does subgroup structure support fair and calibrated modelling?

Yet many teaching datasets fail at this stage — either because they are too small or too unrealistic; </br>
PRIME-CVD Data Asset 1 is deliberately constructed to solve this problem.

It preserves:

* realistic socioeconomic gradients (via IRSD quintiles),
* clinically plausible distributions,
* and genuine class imbalance,

while remaining fully safe for assessment use.

This makes it particularly well-suited to assignments that test judgement, not just code execution.

---

## From Dataset to Assignment: A Canonical Use Case

One of the most reliable ways to assess applied competence is to ask students to stratify a cohort and validate its distributions.

Using Data Asset 1, instructors can pose an assignment that requires students to:

1. Stratify a cardiovascular cohort by [Index of Relative Socioeconomic Disadvantage (IRSD)](https://www.abs.gov.au/ausstats/abs@.nsf/Lookup/by%20Subject/2033.0.55.001~2016~Main%20Features~IRSD~19).
2. Summarise distributions of demographic, behavioural, clinical, and outcome variables.
3. Produce a single, coherent, multi-panel figure suitable for an academic appendix.
4. Interpret what the observed gradients imply for downstream modelling and fairness.

This mirrors exactly what analysts must do when validating EMR-derived cohorts in practice.

---

## What the Expected Output Looks Like

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog03_Fig01.png" width="800"/>

The canonical solution to this task is an IRSD-stratified distributional panel, combining:

* Boxplots for continuous variables (age, BMI, SBP, eGFR, HbA1c, follow-up time),
* Stacked bar plots for smoking status,
* Binary distribution plots for diabetes, CKD, AF, and 5-year CVD events,

with IRSD quintile (1 = most disadvantaged, 5 = least disadvantaged) on the x-axis of every panel.

---

## Why This Works Well for Teaching and Marking

From an educator’s perspective, this style of task has several advantages:

* Clear expectations:
  There is an unambiguous shape to a correct answer.

* Multiple skills assessed simultaneously:
  Stratification, visualisation, data typing, and interpretation are all tested.

* Natural differentiation:
  Strong students demonstrate cleaner figures and sharper interpretations without needing trick questions.

* Alignment with real practice:
  The task mirrors how analysts validate cohorts before fitting risk models.

Because the data are simulated from a known causal structure, instructors can also explain *why* certain gradients appear — or do not — without breaching patient privacy.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-12)
