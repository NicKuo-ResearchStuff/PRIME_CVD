# Lasso Blog 02</br>when ranking shifts more than coefficients

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog18_Sparse2.png" width="600"/>

Hey, hello, and Kia Ora!

[Last time](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A006_ToLassoOrNotToLasso/BlogSparse01), we talked about something very practical:
* FULL model → everything we can measure
* Sparse model → what we can realistically deploy

Today we go one layer deeper.

Because once we have more than one reasonable model, we also need to ask:</br>
Do they actually change how patients are ranked?

And that’s where reclassification — and percentile-NRI — enters the picture.

---

## Beyond coefficients: what actually changes?

Suppose:
* FULL model includes 28 variables
* Sparse model includes 12 variables

Both are stable.
Both are well calibrated.
C-index differs only slightly.

So what?

The deeper question is:</br>
Does the choice of model change who appears high-risk?

Because clinical consequences are not driven by:
* coefficient magnitude
* p-values
* log-likelihood

They are driven by:
* Patient ranking
* Risk ordering
* Movement across the distribution

If adding variables changes how individuals are ordered, then that matters.</br>
Even if the C-index moves by only 0.01.

---

## From discrimination to reclassification

The C-index measures: $P(\hat{r}_i > \hat{r}_j \mid T_i < T_j)$

That is:</br>
Probability that the individual who experiences the event earlier</br>
has a higher predicted risk.

It is a pairwise ranking metric.

But it does not tell us:
* Whether individual A moves meaningfully upward
* Whether true cases are concentrated more strongly in upper risk percentiles
* Whether model choice changes who lands in the top decile

That’s where Net Reclassification Improvement (NRI) comes in.

---

## What is Percentile-NRI?

Traditional NRI works with fixed clinical thresholds, such as:
* <5%
* 5–10%
* ≥10%

But thresholds are arbitrary and unstable.

Percentile-NRI avoids that.

Instead, we:
* Compute predicted risk under Model A and Model B.
* Rank individuals by predicted risk.
* Divide the ranked distribution into $K$ equal-sized bins
* Observe movement between bins.

Let:
* $U_e$ = proportion of event cases moving upward under Model B
* $D_e$ = proportion of event cases moving downward
* $U_n$ = proportion of non-events moving upward
* $D_n$ = proportion of non-events moving downward

Then:

* $\text{NRI}_{event} = U_e - D_e$

* $\text{NRI}_{nonevent} = D_n - U_n$

and the total NRI is the sum of the two above.

Interpretation:

* Positive event-NRI → true cases shifted upward
* Positive non-event NRI → true non-cases shifted downward
* Positive total NRI → improved ordering

This isn't about discrimination in abstract pairs, but rather re-ranking at a distributional level.

In the next next blog, we will implement the percentile-NRI idea to compare the FULL vs Sparse model.

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-24)
