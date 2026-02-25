# PRIME-CVD Data Asset 1:</br> A Clean, Causal Cohort for Teaching Cardiovascular Risk Modelling

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog01.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we introduce PRIME-CVD Data Asset 1, a clean, analysis-ready simluated cohort designed specifically for teaching cardiovascular risk modelling, exploratory data analysis, and causal reasoning in medical informatics.</br>
Unlike toy datasets, PRIME-CVD preserves realistic population structure, socioeconomic gradients, and clinically meaningful imbalance -- while remaining fully safe for classroom use.

This post mirrors how we introduce the dataset live in class: by inspecting its shape, columns, and distributions before doing any modelling.

---

## Data Provenance

PRIME-CVD is a fully simulated cohort, generated de novo from a hand-specified causal directed acyclic graph (DAG) parameterised using publicly available Australian population statistics (ABS, AIHW) and published epidemiologic effect estimates.</br>

No real patient-level electronic medical record (EMR) data are used at any stage. Every individual, covariate, and outcome is simulated deterministically from aggregate priors, ensuring negligible disclosure risk while preserving realistic joint structure.

Data Asset 1 represents a primary-prevention cardiovascular population of 50,000 simulated adults, designed to resemble contemporary EMR-based cohorts used in 5-year CVD risk modelling studies.

---

## A Glimpse of the Data

We begin our live classroom by looking at the top few rows

```python
print("\n" + "###===###"*5)
print("DataAsset1_preview")
df.head()
```

```
###===######===######===######===######===###
DataAsset1_preview
   IRSD_quintile        Age smoking_status        BMI  diabetes  CKD        HbA1c       eGFR         SBP  AF  cvd_event  cvd_time
0              4  50.395265            non  28.166346         0    0     4.317890  83.077560  118.668194   0          1  2.963423
1              3  39.226761             ex  16.825992         0    0     4.700951  81.488401  123.719732   0          0  4.407252
2              5  55.489004            non  23.523419         0    0     3.669685  86.779230  126.650517   0          0  4.490739  
3              4  51.910529            non  31.981932         0    0     4.486977  94.704093  113.889670   0          0  4.888965 
4              1  47.091570             ex  25.351159         0    0     4.315440  86.336256  125.912615   0          0  4.490326 
```

Each row corresponds to one simulated individual, with one-row-per-patient structure suitable for immediate exploratory analysis and survival modelling.

---

## Baseline Variable Structure

The cohort is intentionally compact, with variables grouped into clear conceptual blocks:

| **Category**                    | **Attribute**          | **Type**      | **Notes**               |
| ------------------------------- | ---------------------- | ------------- | ----------------------- |
| **Demographic & Socioeconomic** | Age                    | Numeric       | Continuous (years)      |
|                                 | IRSD quintile          | Ordinal (1–5) | Area-level disadvantage |
| **Behavioural**                 | Smoking status         | Categorical   | non / ex / current      |
| **Anthropometric**              | Body mass index (BMI)  | Numeric       | kg/m²                   |
| **Chronic Conditions**          | Diabetes               | Binary        | 0 / 1                   |
|                                 | Chronic kidney disease | Binary        | 0 / 1                   |
|                                 | Atrial fibrillation    | Binary        | 0 / 1                   |
| **Physiological Measures**      | HbA1c                  | Numeric       | %                       |
|                                 | Systolic BP            | Numeric       | mmHg                    |
|                                 | eGFR                   | Numeric       | mL/min/1.73m²           |
| **Outcome**                     | CVD event              | Binary        | 5-year event            |
|                                 | Follow-up time         | Numeric       | years                   |

This design allows students to immediately distinguish:

* exposures vs outcomes,
* baseline risk factors vs biomarkers,
* and covariates suitable for adjustment vs stratification.

---

## Distributions and Plausibility

Before fitting any models, we examine univariate distributions -- a habit we explicitly teach.</br>
Histograms and boxplots reveal:

* Age: approximately normal, centred around mid-life, bounded at 18–90
* BMI: right-skewed, with realistic upper tails
* SBP: bell-shaped with hypertensive extremes
* eGFR: left-skewed decline consistent with ageing and CKD
* HbA1c: bimodal structure reflecting diabetic vs non-diabetic subpopulations
* Follow-up time: concentrated near 5 years with administrative censoring

An example code is attached to this folder for supporting discussions about robustness, transformation, and data quality checks.

---

## Categorical Structure and Imbalance

PRIME-CVD is not class-balanced, by design.

```
──────────────────────────────────────────────────────────────
    Diabetes (Yes) ................. ~7 %
    CKD (Yes) ...................... <1 %
    AF (Yes) ....................... <1 %
    Current smokers ................ ~10 %
    CVD events (5-year) ............ ~4 %
──────────────────────────────────────────────────────────────
```

This imbalance reflects real primary-prevention populations and provides a natural setting to discuss:

* rare-event modelling,
* calibration,
* and subgroup-specific risk.

Students quickly see why naive accuracy metrics fail in this context.

---

## Missingness and Data Quality

Although Data Asset 1 is “clean”, it is not perfect.</br>
Studnets must apply their knowledge to:
* identify columns with any missing values,
* prioritise clinically important variables,
* and decide which fields require extra wrangling before modelling.

---

## Teaching Philosophy

PRIME-CVD Data Asset 1 represents what analysts wish they had:

* one row per patient,
* coherent variable naming,
* known causal structure,
* and transparent assumptions.

It exists to let students focus on:

* exploratory data analysis,
* stratification,
* survival modelling,
* and interpretation -- before confronting EMR chaos.

In later labs, students work backwards from the relational EMR representation to recover this structure, reinforcing the full analytic lifecycle.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-08)
