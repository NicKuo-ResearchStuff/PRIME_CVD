# Discrimination Blog 03</br>Binary discrimination: details and interpretation

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog11_D3.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we examine binary discrimination in detail —</br> 
what question it answers and what its metrics emphasise.

---

## From Time-to-Event Data to a Binary Outcome

Binary discrimination begins by collapsing survival data into a single indicator:

* event occurred, or
* event did not occur.

Formally, each individual is reduced to:</br>
$\texttt{cvd event} \in {0, 1}$

Under this abstraction:

* event time is discarded,
* censoring is ignored,
* follow-up length is ignored.

All individuals without an observed event are treated as equivalent.

---

## From Risk Scores to Metrics: What to Focus on in the Code

We provide the full PRIME-CVD implementation alongside this post.</br>
You do not need to understand every line.

For this blog, focus on the following block:

```python
threshold = np.median(train_risk)

y_pred_test = (test_risk >= threshold).astype(int)

accuracy  = accuracy_score(y_event_test, y_pred_test)
precision = precision_score(y_event_test, y_pred_test, zero_division=0)
recall    = recall_score(y_event_test, y_pred_test, zero_division=0)
f1        = f1_score(y_event_test, y_pred_test, zero_division=0)

auroc = roc_auc_score(y_event_test, test_risk)
auprc = average_precision_score(y_event_test, test_risk)
```

Conceptually, this block does three things:

* converts continuous risk scores into binary predictions using a threshold,
* evaluates threshold-dependent metrics (accuracy, precision, recall, F1),
* evaluates threshold-free ranking metrics (AUROC, AUPRC).

Everything that follows in this post is about interpreting the outputs of this block.

The code is provided in the same folder as this blog.

---

## What Binary Metrics Emphasise

Different binary metrics answer different questions.</br>
* Accuracy: How often is the model correct overall?
* Precision: Among predicted events, how many are true events?
* Recall (Sensitivity): Among true events, how many were identified?
* F1-score: How balanced is the trade-off between precision and recall?

Each metric encodes a different value judgement; refer to details in [the previous blog](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A003_DiscriminationBlogs/BlogD02).

## Threshold-Free Discrimination

Furthermore, AUROC and AUPRC both evaluate discrimination without fixing a threshold.</br>
However, they emphasise different aspects of performance.
* AUROC: measures how well the model ranks event cases above non-event cases across all possible thresholds.
* AUPRC: summarises the trade-off between precision and recall, focusing explicitly on the event class.

When events are rare - as they are for CVD - these metrics can tell very different stories.

---

## PRIME-CVD Example Output

Using the PRIME-CVD test set, binary discrimination yields:

```
=== Test-set binary discrimination ===
Accuracy : 0.543
Precision: 0.076
Recall   : 0.930
F1-score : 0.141
AUROC    : 0.879
AUPRC    : 0.420
```

Here:
* AUROC suggests strong ranking performance,
* recall is high,
* precision is low,
* accuracy is modest.

---

## Where We’re Going Next

In the next post, we return to the same cohort, the same model, and the same risk scores — but we stop ignoring time.

We ask a refined question:</br>
Does the model assign higher risk to individuals who experience events earlier?

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-30)
