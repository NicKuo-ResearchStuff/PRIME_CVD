# Discrimination Blog 02</br> A reference for discrimination metrics

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog10_D2.png" width="600"/>

The purpose of this post is simple: to provide a single, stable place where all discrimination-related quantities used in this series are defined in a consistent way. Rather than reintroducing definitions repeatedly in later posts, this page serves as a reference glossary for confusion-matrix counts, discrimination metrics, and survival-specific measures, including their mathematical meaning, interpretation, and corresponding Python implementations. You are not expected to read this post linearly; instead, think of it as a resource to return to whenever a term or metric needs clarification.

Cheers, <br>
\- Nic

(Last edit: 2026-01-29)

---

## Confusion-matrix primitives

(counts, not metrics)

---

### True Positive (TP)

1. An individual who truly had the event and was correctly predicted to have it.

2. $TP = |{ i : y_i = 1 \ \text{and} \ \hat{y}_i = 1 }|$

3. Interpretation: A raw count; no "better" or "worse" in isolation (Range: [0, N])

4. `sklearn.metrics.confusion_matrix`

---

### False Positive (FP)

1. An individual who did not have the event but was incorrectly predicted to have it.

2. $FP = |{ i : y_i = 0 \ \text{and} \ \hat{y}_i = 1 }|$

3. Interpretation: A raw count of false alarms (Range: ([0, N])).

4. `sklearn.metrics.confusion_matrix`

---

### True Negative (TN)

1. An individual who did not have the event and was correctly predicted not to have it.

2. $TN = |{ i : y_i = 0 \ \text{and} \ \hat{y}_i = 0 }|$

3. Interpretation: A raw count of correct non-events (Range: ([0, N])).

4. `sklearn.metrics.confusion_matrix`

---

### False Negative (FN)

1. An individual who had the event but was incorrectly predicted not to have it.

2. $FN = |{ i : y_i = 1 \ \text{and} \ \hat{y}_i = 0 }|$

3. Interpretation: A raw count of missed events (Range: ([0, N])).

4. `sklearn.metrics.confusion_matrix`

---

## Binary classification metrics

(threshold-dependent)

---

### Accuracy

1. The fraction of all predictions that are correct.

2. $\text{Accuracy} = \dfrac{TP + TN}{TP + TN + FP + FN}$

3. Interpretation: Higher is better (Range: ([0, 1]); 1 = perfect classification, 0 = completely incorrect).

4. `sklearn.metrics.accuracy_score`

---

### Precision

1. Among predicted events, how many truly had the event.

2. $\text{Precision} = \dfrac{TP}{TP + FP}$

3. Interpretation: Higher is better (Range: ([0, 1]); 1 = no false positives, 0 = all predicted events are wrong).

4. `sklearn.metrics.precision_score`

---

### Recall (Sensitivity)

1. Among true events, how many the model correctly identified.

2. $\text{Recall} = \dfrac{TP}{TP + FN}$

3. Interpretation: Higher is better (Range: ([0, 1]); 1 = no missed events, 0 = all events missed).

4. `sklearn.metrics.recall_score`

---

### F1-score

1. A single score balancing precision and recall.

2. $\text{F1} = 2 \cdot \dfrac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$

3. Interpretation: Higher is better (Range: ([0, 1]); 1 = perfect precision and recall, 0 = one of them is zero).

4. `sklearn.metrics.f1_score`

---

## Binary discrimination / ranking metrics

(threshold-free, time ignored)

---

### AUROC (Area Under the ROC Curve)

1. How well the model ranks event cases above non-event cases.

2. $\text{AUROC} = \Pr\big( s(X^+) > s(X^-) \big)$

3. Interpretation: Higher is better (Range: ([0, 1]); 0.5 ≈ random ranking, 1 = perfect ranking).

4. `sklearn.metrics.roc_auc_score`

---

### AUPRC (Area Under the Precision–Recall Curve)

1. Overall trade-off between precision and recall across all thresholds.

2. $\text{AUPRC} = \int_0^1 \text{Precision}(r), d,\text{Recall}(r)$

3. Interpretation: Higher is better (Range: ([0, 1]); baseline ≈ event prevalence, 1 = perfect precision and recall everywhere).

4. `sklearn.metrics.average_precision_score`

---

## Time-to-event (survival) discrimination metrics

---

### Harrell’s C-index

1. How often individuals who experience events earlier are ranked as higher risk.

2. $C = \Pr\big( s_i > s_j \mid T_i < T_j,\ \delta_i = 1 \big)$

3. Interpretation: Higher is better (Range: ([0, 1]); 0.5 ≈ random ordering, 1 = perfect concordance).

4. `lifelines.utils.concordance_index`

---

### Time-dependent AUC

(Cumulative Dynamic AUC)

1. How well predicted risks separate failures from survivors at a specific time point.

2. $\text{AUC}(t) = \Pr\big( s(X^+_t) > s(X^-_t) \big)$

3. Interpretation: Higher is better (Range: ([0, 1]); 0.5 ≈ no discrimination at time (t), 1 = perfect discrimination at time (t)).

4. `sksurv.metrics.cumulative_dynamic_auc`

---

## Model outputs used by metrics

(not metrics)

---

### Risk score / predicted score

1. A number indicating relative risk for each individual.

2. $s_i = f(x_i)$

3. Interpretation: Scale is arbitrary; only ordering matters for discrimination.

4. Model-specific (e.g. `predict_proba`, `decision_function`, Cox outputs)

---

### Partial hazard

1. Relative risk output from a Cox proportional hazards model.

2. $\exp(\beta^\top x_i)$

3. Interpretation: Positive real values; not a probability; used only for ranking.

4. `lifelines.CoxPHFitter.predict_partial_hazard`
