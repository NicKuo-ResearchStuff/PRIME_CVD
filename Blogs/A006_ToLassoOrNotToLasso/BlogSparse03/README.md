# Lasso Blog 03</br>implementation NRI

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog19_Sparse3.png" width="600"/>

Hey, hello, and Kia Ora!

[Last time](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A006_ToLassoOrNotToLasso/BlogSparse02), we introduced percentile-NRI as the “ranking-aware” companion to C-index:</br>
not how well the model discriminates on average, but</br>
whether it actually reshuffles who ends up in the top decile.

Today we do the promised thing:
* implement percentile-NRI,
* show what the code is really doing,
* and interpret the FULL vs Sparse (LASSO) results with the movement tables.

---

## The one rule of NRI: you must define “truth” at a horizon

Percentile-NRI is a horizon-based concept.</br>
So before we count “up” or “down”, we have to answer:</br>
At 5 years, do we know this person is an event or a non-event?

In the implementation, that is the key design choice:

```python
is_event_by_t0 = (event == 1) & (time <= t0)
is_known_nonevent_by_t0 = (time >= t0)

eligible = is_event_by_t0 | is_known_nonevent_by_t0
```

Why exclude the censored-before-horizon group?</br>
Because at 5 years we genuinely don’t know what would have happened.</br>
If you keep them in, you accidentally reward whichever model pushes censored people downward.

---

## Percentiles are not thresholds but ranks

Once eligibility is set, the code does this:

```python
rank_a = risk_a.rank(method="average")
rank_b = risk_b.rank(method="average")

bin_a = qcut(rank_a, q=K)
bin_b = qcut(rank_b, q=K)
```

Interpretation:
* We are not comparing absolute risk values.</br>
  (Those might differ by calibration, baseline survival, etc.)
* We are comparing ordering.</br>
  Who lands in top 10%, middle 10%, bottom 10%.

When we set `K=10` (*i.e.,* deciles), “moving up” means:</br>
Under LASSO, you now sit in a higher risk decile than you did under FULL.

---

## Movement direction: “up” and “down” depend on who you are

Then we assign movement:

```python
move = "up"   if bin_b > bin_a
move = "down" if bin_b < bin_a
move = "same" otherwise
```

Now comes the key asymmetry:

For events (true cases): up = good; down = bad

For non-events (true non-cases): down = good; up = bad

That’s why NRI is split:

* NRI_event = Ue − De
* NRI_nonevent = Dn − Un

---

## We found that: sparse ranking got worse, not better

```
Eligible n = 22458
Event by t0 n = 1941
Non-event at t0 n = 20517

NRI_event    = -0.0088
NRI_nonevent = -0.0248
NRI_total    = -0.0335
```

In plain language:</br>
At 5 years, switching from FULL → LASSO causes a net worsening of decile reclassification by ~3.35%;</br>
and the harm is mostly from the non-event side.

Or for our case, we found that:</br>
sparsification didn’t just “remove weak variables”; </br>
it changed ordering in a way that pushes more true non-cases upward.

---

## The movement tables

Percentile-NRI is a summary statistic.</br>
The movement table shows you how it happens.

### Event movement table (FULL bin → LASSO bin)

You posted:

```
9 → 9 : 1171
8 → 8 : 202
7 → 7 : 69
6 → 6 : 42
...
9 → 8 : 30
8 → 7 : 31
7 → 6 : 35
```

The visual takeaway:

#### 1) The top is stable

Most event cases stay in the upper tail.</br>
`(9→9)=1171` is enormous.

So LASSO didn’t destroy the model.

#### 2) The drift is downward at the boundary

The net loss comes from small but systematic “down moves”:

* FULL bin 9 events can’t move up (ceiling effect), only stay or drop.</br>
  You have `9→8=30` and `9→7=1`.
* FULL bin 8 events show more drop than rise:</br>
  `8→9=18` (good), but `8→7=31` (bad) plus smaller additional drops.

So the event-NRI being slightly negative makes sense:</br>
not a collapse, but a mild erosion in the high-risk boundary.

---

## What to check next

If this were a real deployment decision, we’d stress-test the result.
1. Relax sparsity</br>
   Try a milder setting (*e.g.,* `l1_ratio = 0.5`). Map sparsity against NRI — there may be a better balance.
2. Check top-decile purity</br>
   How many non-events sit in decile 9 under each model? NRI shows direction; purity shows operational impact.
3. Bootstrap NRI</br>
   Estimate a 95% CI. If −0.033 remains consistently below zero, the ranking loss is structural, not noise.

The real question isn’t whether LASSO is “good” — it’s how much ranking change you’re willing to trade for deployability.

---

Cheers,</br>
\- Nic

(Last edit: 2026-03-04)
