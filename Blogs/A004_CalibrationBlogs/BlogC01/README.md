# Calibration Blog 01</br>probability honesty in survival models

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog13_C1.png" width="600"/>

Hey, hello, and Kia Ora!

In the previous post, we evaluated whether the model ranks individuals correctly in time.

Now we keep the same PRIME-CVD cohort,
the same Cox model,
and the same predicted risk scores —

but we stop asking about ranking.

---

## The Core Idea

Calibration is probability honesty.

In a CoxPH model, the raw output (LPH / linear predictor) is not a probability — it is a log–relative hazard.

To talk about calibration, we must first move from the hazard scale to the probability scale at a chosen time horizon $ t $:

$\text{LPH}_i \to S_i(t) = [S_0(t)]^{\exp(\text{LPH}_i)} \to \hat r_i(t) = 1 - S_i(t).$

Now we have:

$\hat r_i(t) \in [0,1],$

a predicted probability of experiencing the event by time $t$.

Calibration asks a single question:</br>
Among people predicted to have risk $r$ by time $t$, do about $r$ of them actually experience the event by time $t$?

Because follow-up differs across individuals, we typically choose evaluation times such as the 25th, 50th, or 75th percentile of follow-up.
This ensures the chosen $t$ is meaningful for most of the cohort.

Discrimination asks whether ordering is correct.
Calibration asks whether probabilities are numerically trustworthy.

---

## The Dictionary

### LPH / linear predictor

$\text{LPH}_i = (X_i - \mu)^\top \beta$

A patient-specific risk score on the hazard scale (not a probability).

---

### Hazard (CoxPH form)
$h_i(t) = h_0(t)\exp(\text{LPH}_i)$

LPH scales the baseline hazard up or down.

---

### Survival probability at time $t$
$S_i(t) = [S_0(t)]^{\exp(\text{LPH}_i)}$

Probability of remaining event-free up to time $t$.

---

### Predicted risk at time $t$
$\hat r_i(t) = 1 - S_i(t)$

Probability of having the event by time $t$.
This is what calibration evaluates.

---
### Observed event indicator by time $t$
$y_i(t) \in {0,1}$

Whether the event has occurred by time $t$ (using the “by $t$” framing).

---
### Perfect calibration
$P(Y(t)=1 \mid \hat r(t)=r) = r$

Predicted probabilities match observed frequencies.

---
### Empirical calibration curve (bin-based)

Sort individuals by $\hat r_i(t)$, split into bins, and compute:
$\big(\overline{\hat r}_k(t),;\overline{y}_k(t)\big)$

Mean predicted risk versus observed event rate per bin.

---
### Calibration slope $\beta(t)$

Regression through the origin:
$\overline{y}_k(t) \approx \beta(t),\overline{\hat r}_k(t)$

* $\beta(t) = 1$ → ideal
* $\beta(t) < 1$ → under-prediction
* $\beta(t) > 1$ → over-prediction

---
### $D_{21}(t)$
$D_{21}(t) = |1 - \beta(t)|$

Distance from perfect calibration (0 is ideal).

---

For those who are interested in more details of calibration and their formal implementation, please consider the following 11-part breakdown:</br>
[1](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part01), [2](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part02), [3](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part03), [4](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part04), [5](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part05), [6](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part06), [7](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part07), [8](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part08), [9](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB002_Part09), [10](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB003_Part01), [11](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_X_Implementation/Blog_CKD_UnderstandingB004_Fin)

In the next blog, we will provide some preliminary code to show how to compute calibration from first principles.

Cheers,</br>
\- Nic

(Last edit: 2026-02-17)
