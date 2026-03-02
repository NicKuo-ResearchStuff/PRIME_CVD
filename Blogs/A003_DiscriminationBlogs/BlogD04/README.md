# Discrimination Blog 04</br>Time-to-event discrimination: details and interpretation

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog12_D4.png" width="600"/>

Hey, hello, and Kia Ora!

In the previous post, we evaluated a survival model as if it were a classifier.
We deliberately ignored event timing and censoring.

Now we return to the same PRIME-CVD cohort,
the same Cox model,
and the same predicted risk scores —

but we stop discarding time.

---

## From Binary Outcomes Back to Survival Data

In [Blog 03](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A003_DiscriminationBlogs/BlogD03), each individual was reduced to:

```
cvd_event ∈ {0,1}
```

All non-events were treated as equivalent.

In survival analysis, that simplification is no longer acceptable.

Each individual instead contributes:

* an event indicator (`cvd_event`), and
* an observed time (`cvd_time`), representing either:

  * time to event, or
  * time to censoring.

Now the question becomes more precise:</br>
Does the model assign higher risk to individuals who experience events earlier?

This is still a ranking question —
but now ranking must respect time and censoring.

---

## What Changes in the Code?

The modelling block does not change.

We still compute continuous Cox partial hazard scores:

```python
test_risk = cph.predict_partial_hazard(X_test_final)
```

What changes is only the evaluation step.

Instead of thresholding the risk score, we compute:

```python
cindex_test = concordance_index(y_time_test, -test_risk, y_event_test)
```

And:

```python
cumulative_dynamic_auc(...)
```

---

## Harrell’s C-index: Global Survival Discrimination

Harrell’s C-index measures:</br>
Among comparable pairs of individuals, how often does the model correctly rank who fails earlier?

We find that

```
Harrell C-index (train): 0.871
Harrell C-index (test) : 0.873
```

Interpretation:

* Approximately 87% of comparable pairs are correctly ordered.
* Train and test performance are nearly identical.
* Discrimination is strong and stable.

---

## Time-Dependent AUC: Local Survival Discrimination

The C-index gives a global summary over follow-up.

Time-dependent AUC asks a different question:
* At a specific time horizon $ t $,
* can the model distinguish individuals who fail before $ t $
* from those who remain event-free at $ t $?

```
AUC(t=4.4) : 0.881
AUC(t=4.7) : 0.875
AUC(t=5.0) : 0.876
AUC(t=5.3) : 0.886
Mean AUC   : 0.881
```

Interpretation:

* Discrimination remains consistently strong across horizons.
* The model separates earlier failures from survivors well.
* Performance is not confined to a single time window.

---

## Comparing Blog 03 and Blog 04

Binary discrimination asked:</br>
“Who ever had an event?”

Time-to-event discrimination asks:</br>
“Who fails earlier?”

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-16)
