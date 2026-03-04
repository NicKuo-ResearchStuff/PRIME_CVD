# Lasso Blog 01</br>when deployment reality meets variable count

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog17_Sparse1.png" width="600"/>

Hey, hello, and Kia Ora!

In this blog, we question:
* Do we want a FULL model that uses everything we can measure,
* or a Sparse model that uses only what we can realistically deploy?

---

## From “Best Possible Data” to “Deployable Data”

In an ideal world, we would build risk models using a huge EMR:

* primary care records,
* hospital admissions,
* pathology systems,
* imaging,
* medication history,
* every measurement we can find.

This is the Christmas-land scenario, because the model gets to see more of the patient.

But clinical deployment is not just modelling; it is more about systems design.

A FULL model that includes hospital lab measurements may require:
* linkage between GP and hospital identifiers,
* governance approvals,
* data sharing agreements,
* disclosure risk management,
* ongoing integration and monitoring.

Whereas a GP-only model might be simpler:
* demographics,
* disease flags,
* smoking,
* maybe a few routine vitals.

So the trade-off is:</br>
More variables → more information → stronger model potential</br>
but also:</br>
More variables → more coordination → harder deployment.

---

## What Changes in the Code?

The dataset and design matrix do not change.</br>
What changes is how we regularise the Cox model.

We fit two versions:
* FULL model: keep all variables in play
* Sparse model: encourage the model to drop weak variables (LASSO)

The key control is in `lifelines.CoxPHFitter`:

```python
PENALIZER = 0.01

# FULL CoxPH
cph_full = CoxPHFitter(penalizer=PENALIZER, l1_ratio=0.0)

# Sparse CoxPH (LASSO-like)
cph_lasso = CoxPHFitter(penalizer=PENALIZER, l1_ratio=0.95)
```

(Full runnable code is included in the same folder as this blog.)

---

## What is `l1_ratio`?

This penalty is an elastic-net mixture:
$-\ell(\beta)+\lambda\left[(1-\alpha)\frac{1}{2}|\beta|_2^2+\alpha|\beta|_1\right]$

Where:

* $\ell(\beta)$ is the Cox partial log-likelihood,
* $\lambda$ is `penalizer`,
* $\alpha$ is `l1_ratio`.

where: $\alpha \in [0,1]$.

Interpretation:
* `l1_ratio = 0.0` → no sparsity pressure (FULL)
* `l1_ratio = 1.0` → pure LASSO (maximum sparsity pressure)
* `0 < l1_ratio < 1` → mostly LASSO, with some ridge stabilisation

---

## What does `PENALIZER` do?

`PENALIZER` is the global shrinkage knob.

* Larger value → coefficients pulled toward 0 → HRs pulled toward 1
* Smaller value → coefficients freer to grow → HRs further from 1

It affects both FULL and Sparse fits.

For numerical stability, we use:

```python
PENALIZER = 0.01
```

for both models — so we are comparing penalty type rather than penalty strength.

Note that we use `l1_ratio = 0.95` in the Sparse model, to encourage numeric stability from the small L2 component.

---

## What does sparsity look like in the output?

The key pattern you will notice in the Sparse model summary is that,</br>
a lot of the hazard ratios “squashed” to 1, or</br>
```
\exp(0)=1
```
meaning that</br>
This variable does not buy enough improvement to justify its complexity.


---

## Visualising FULL vs Sparse HRs

To make this intuitive, we plot the hazard ratios side-by-side:
* blue dots (FULL) spread out across the HR axis,
* orange dots (Sparse) pulled back toward HR = 1 for many covariates.

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog17_Sparse1_Fig01.png" width="600"/>

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-23)
