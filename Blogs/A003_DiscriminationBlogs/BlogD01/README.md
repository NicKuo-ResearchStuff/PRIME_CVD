# Discrimination Blog 01</br>Overall idea of discrimination

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog09_D1.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we introduce the core idea of discrimination — what it means and why it deserves careful treatment.

---

## A Single Question That Unifies Discrimination

Discrimination questions:</br>
*Given two individuals, can the model correctly rank who is at higher risk?*</br>
At its core, discrimination asks whether a model produces a sensible ordering of individuals by risk.

---

## Discrimination Is About Ranking, Not Probability

Most predictive models in health produce some form of [continuous score](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_Z_Implementation/Implementation03):
* a predicted probability,
* a linear predictor,
* a relative risk,
* or a partial hazard.

For discrimination, the scale of this score is irrelevant.</br>
What matters is only the ordering:</br>
who is ranked higher, and who is ranked lower.

Hence it is not probability:</br>
If every score were multiplied by ten, discrimination would not change.

---

## Two Ways Discrimination Commonly Appears in Practice

Although discrimination always reduces to ranking, it is commonly framed in two different ways, depending on how outcomes are defined.

### Binary Discrimination: Ignoring Time

In a binary setup, each individual is reduced to a single outcome:

* event occurred, or
* event did not occur.

The question becomes:</br>
*Can the model rank people who experienced the event above those who did not?*

This framing dominates introductory machine learning and classification settings.</br> 
Metrics such as accuracy, precision, recall, AUROC, and AUPRC all live comfortably here.

Binary discrimination is often pedagogically useful — but it implicitly discards information about when events occur.

---

### Time-to-Event Discrimination: Respecting Time

In time-to-event (survival) settings, outcomes include both:

* whether an event occurred, and
* when it occurred (or when observation stopped).

Here, discrimination asks a more refined question:</br>
*Does the model assign higher risk to individuals who experience events earlier?*

This framing acknowledges that:
* not all individuals are observed for the same length of time,
* some individuals are censored,
* and not all comparisons are valid.

Metrics such as Harrell’s C-index and time-dependent AUC exist precisely because binary discrimination breaks down once time and censoring are taken seriously.

---

## How PRIME-CVD Fits Into This Picture

PRIME-CVD is designed to support this progression.

Its clean cohort asset allows instructors to:

* demonstrate binary discrimination in a controlled setting, and then
* reintroduce time and censoring without changing the underlying population.

This makes it particularly well-suited for teaching why different discrimination metrics exist, rather than simply how to compute them.


---

## Where We’re Going Next

This post has deliberately avoided technical detail.

In the next entries, we will:

* define all discrimination-related terms in one place,
* examine binary discrimination metrics in depth,
* and then move carefully into time-to-event discrimination.

Throughout, we will return to the same unifying question:</br>
*Given two individuals, can the model correctly rank who is at higher risk?*

That question is the conceptual anchor for everything that follows.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-28)
