# PRIME-CVD Data Asset 1:</br>Understanding Baseline Patients and Cox Models</br>with a Clean CVD Cohort

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog06.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we show how PRIME-CVD Data Asset 1 can be used to teach Cox proportional hazards model(see [[1]](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_Z_Implementation/Implementation03) & [[2]](https://github.com/NicKuo-ResearchStuff/Masked_Clinical_Modelling/tree/main/Blogs/Blogs_Z_Implementation/Implementation04)).

In particular, we focus on:

* what a baseline patient actually is,
* how variable coding choices define that baseline,
* and why these decisions matter when moving from teaching datasets to real-world electronic medical records (EMRs).

This entry is written for educators and students working in postgraduate health science, medical informatics, epidemiology, or applied data science.

An example CoxPH modelling script is included in the same folder as this blog.
Students are encouraged to read the code alongside this post.

---

## Fitting the Cox Model

Students can learn to fit a CoxPH model using the widely adopted `lifelines` library on our [PRIME-CVD Data Asset 1](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A001_DataAssetDemonstration/SubBlog02).

We begin by importing the library:

```python
from lifelines import CoxPHFitter
```
Then fit the model:
```python
cph = CoxPHFitter()

cph.fit(
    cox_df,
    duration_col="cvd_time",
    event_col="cvd_event"
)
```

Here:

* `cvd_time` is the follow-up time (in years),
* `cvd_event` indicates whether a cardiovascular event occurred.

Once the model is fitted, the students can extract relevant information, such as:

* hazard ratios (HR),
* 95% confidence intervals,
* and p-values.

via

```python
hr_table = cph.summary[[
    "exp(coef)",
    "exp(coef) lower 95%",
    "exp(coef) upper 95%",
    "p"
]].rename(columns={
    "exp(coef)": "HR",
    "exp(coef) lower 95%": "HR_lower_95",
    "exp(coef) upper 95%": "HR_upper_95",
    "p": "p_value",
})

print("\nHazard ratios (baseline: non-smoker, IRSD 5):")
print(np.round(hr_table, 2))
```
to dervie the results shown below:

| Covariate     | HR   | HR (95% CI) Lower | HR (95% CI) Upper | p-value |
| ------------- | ---- | ----------------- | ----------------- | ------- |
| Age_c         | 1.03 | 1.03              | 1.03              | 0.00    |
| AF            | 2.90 | 2.24              | 3.75              | 0.00    |
| CKD           | 0.97 | 0.75              | 1.26              | 0.84    |
| Diabetes      | 4.15 | 3.77              | 4.57              | 0.00    |
| HbA1c         | 1.37 | 1.33              | 1.41              | 0.00    |
| BMI           | 1.01 | 1.01              | 1.02              | 0.00    |
| eGFR          | 0.98 | 0.98              | 0.99              | 0.00    |
| SBP           | 1.01 | 1.01              | 1.01              | 0.00    |
| smoke_current | 1.18 | 1.08              | 1.30              | 0.00    |
| smoke_ex      | 1.17 | 1.08              | 1.26              | 0.00    |
| irsd_1        | 1.00 | 0.93              | 1.07              | 0.92    |
| irsd_2        | 1.04 | 0.96              | 1.13              | 0.36    |
| irsd_3        | 1.05 | 0.98              | 1.12              | 0.19    |
| irsd_4        | 0.99 | 0.91              | 1.07              | 0.82    |

---

## The Core Idea: Everything Is Relative to a Baseline Patient

[Real world healthcare professionals](https://heart.bmj.com/content/early/2025/11/17/heartjnl-2025-325776.abstract) estimate 5-year cardiovascular disease (CVD) risk using a Cox proportional hazards model.

Every modelling choice the students see in the example code exists only to define that reference clearly.

The baseline patient in the PRIME-CVD Cox model is:</br>
A 30-year-old,</br>
non-smoker,</br>
living in the least disadvantaged (IRSD 5) area,</br>
with no AF, no CKD, no diabetes,</br>
and baseline biomarker values.

Let us look at some details below.

---

### Why Do We Use `Age − 30`?

In the example code, students will see:

```python
df["Age_c"] = df["Age"] - 30
```

This means age is interpreted as: Per additional year above age 30.

So:

* Age 30 → `Age_c = 0`
* Age 40 → `Age_c = 10`
* Age 60 → `Age_c = 30`

This does not change the fitted model.</br>
It changes how we interpret it, to avoid the meaningless idea of “risk at age zero”.


---

### Why Are AF, CKD, and Diabetes Coded as 0/1?

In PRIME-CVD Data Asset 1, the variables:

* atrial fibrillation (AF),
* chronic kidney disease (CKD),
* diabetes,

are coded as binary indicators:

| Value | Meaning           |
| ----- | ----------------- |
| 0     | Condition absent  |
| 1     | Condition present |

In a Cox model:

* `0` represents the baseline state
* `1` represents an added hazard multiplier

So if the output reports:

```
HR(AF) = 2.8
```

This means: A patient with AF has 2.8× the hazard of an otherwise identical patient without AF.

---

## From Teaching Data to Real EMRs

The example code provided with this post shows a complete, reproducible CoxPH implementation.

Students are strongly encouraged to:

* read the code,
* map each variable back to this explanation,
* and then look up the [papers](https://heart.bmj.com/content/early/2025/11/17/heartjnl-2025-325776.abstract) to see how these same modelling ideas behave when applied to real, messy healthcare data.

PRIME-CVD exists to prepare students for that transition -- safely, transparently, and without governance barriers.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-15)
