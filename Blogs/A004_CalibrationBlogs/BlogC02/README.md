# Calibration Blog 02</br>Empirical calibration and the slope $\beta(t)$

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog14_C2.png" width="600"/>

Hey, hello, and Kia Ora!

In the previous post, we defined calibration conceptually:</br>
Are predicted probabilities numerically honest?

Now we move from definition to implementation.

We keep:

* the same PRIME-CVD cohort,
* the same Cox proportional hazards model,
* the same predicted risks $\hat r_i(t)$,

but we now unpack exactly how empirical calibration is constructed — and what the calibration slope $\beta(t)$ really means.

---

## From Individual Predictions to Bin-Level Comparison

At a chosen time horizon $t = 4.88$, we already computed:

$\hat r_i(t) = 1 - S_i(t)$

and

$y_i(t) = \mathbf{1}{ \text{event occurred by time } t }.$

So for each individual we have:
* a predicted probability $\hat r_i(t) \in [0,1]$,
* an observed indicator $y_i(t) \in {0,1}.$

Calibration asks whether these agree — but we do not observe $P(Y(t)=1 \mid \hat r(t)=r)$ directly.

So we approximate it.

---

## Step 1 — Sort by Predicted Risk

```python
tmp = pd.DataFrame({"risk": risk_t, "y": y_by_t}) \
        .sort_values("risk") \
        .reset_index(drop=True)
```

We first order individuals from lowest to highest predicted probability.

This ordering is purely model-driven.

Observed outcomes are not used yet.

---

## Step 2 — Create Equal-Count Risk Bins

```python
tmp["bin"] = pd.qcut(tmp["risk"], q=K, duplicates="drop")
```

This line creates $K$ bins based on quantiles of predicted risk.

If $K = 20$:

* Lowest 5% risk → bin 1
* Next 5% → bin 2
* …
* Highest 5% → bin 20

Each bin contains roughly the same number of individuals.

---

## Step 3 — Compare Predicted vs Observed Within Each Bin

```python
g = tmp.groupby("bin", observed=False)

r_bar = g["risk"].mean().to_numpy(float)
y_bar = g["y"].mean().to_numpy(float)
```

Now the key objects emerge:
$\overline{\hat r}_k(t)
\quad \text{and} \quad
\overline{y}_k(t).$

For each bin ( k ):

* $\overline{\hat r}_k(t)$ = mean predicted risk
* $\overline{y}_k(t)$ = observed event rate

Each pair

$\big(\overline{\hat r}_k(t),\ \overline{y}_k(t)\big)$

is one point on the empirical calibration curve.

---

## The Calibration Plot at ( t = 4.88 )

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog14_Fig01.png" width="300"/>

The resulting plot shows:

* Blue dots → bin-level predicted vs observed
* Dashed 45° line → perfect calibration ( y = x )
* Blue line → fitted slope ( y = a x )

For our example:

$\text{calibration slope (a)} = 1.161 \quad\text{and}\quad D_{21}(t) = |1 - a| = 0.161.$

---

## Interpreting $a = 1.161$

Because:
$a > 1,$

the fitted line is steeper than the 45° line.

This means (with predicted risk on the y-axis):</br>
Predicted event rates are a tad higher than observed risks.

In plain language:
The model is over-predicting absolute risk at $t = 4.88$.

---

## Why Most Points Cluster Near Zero

CVD events are rare.

Even by time 4.88:
* Most predicted probabilities are small.
* Most observed event rates are small.

So most bins lie near the origin.

This is expected in low-prevalence settings.

---

## Code

The full implementation used to generate the calibration curve and slope is attached in the same folder as this blog.

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-18)
