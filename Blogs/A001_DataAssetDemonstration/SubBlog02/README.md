# PRIME-CVD Data Asset 1:</br> Synthetic Cohort Characteristics and Baseline Structure

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog02.png" width="600"/>

Hey, hello, and Kia Ora!

This post documents the baseline characteristics and structural properties of PRIME-CVD Data Asset 1, a clean, analysis-ready synthetic cohort designed to support cardiovascular risk modelling, methodological development, and reproducible education.

Unlike the companion teaching blog, which focuses on how students interact with the dataset, this entry serves as data documentation: it summarises cohort composition, variable distributions, and outcome frequencies in a form suitable for citation, validation, and downstream reuse.

---

## Cohort Overview

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog02_Fig01.png" width="800"/>

PRIME-CVD Data Asset 1 comprises 50,000 simulated adults aged 18–90 years, representing a primary-prevention cardiovascular population.

The cohort was generated de novo from a hand-specified causal directed acyclic graph (DAG), parameterised using publicly available Australian population statistics (ABS, AIHW) and published epidemiologic effect estimates. No real patient-level data are used.

Key demographic properties include:
* Age
  * Mean (SD): 49.71 (12.37) years
  * Median [IQR]: 49.63 [41.33, 58.09]
  * Range: 18.0–90.0
* Socioeconomic position (IRSD quintile)
  * Q1 (most disadvantaged): 21.28%
  * Q2: 16.11%
  * Q3: 23.88%
  * Q4: 16.99%
  * Q5 (least disadvantaged): 21.74%

This balance ensures that socioeconomic gradients can be examined without extreme sparsity while still preserving realistic population structure.

---

## Behavioural and Chronic Disease Profile

Baseline behavioural and clinical variables reflect contemporary primary-care prevention cohorts:
* Smoking status
  * Non-smoker: 73.14%
  * Ex-smoker: 16.72%
  * Current smoker: 10.13%
* Chronic disease prevalence
  * Diabetes mellitus: 7.43%
  * Chronic kidney disease (CKD): 0.68%
  * Atrial fibrillation (AF): 0.72%

Low prevalences of CKD and AF are intentional, mirroring their rarity in general primary-prevention populations and providing a realistic setting for rare-event modelling and subgroup analysis.

---

## Anthropometric and Physiological Measurements

Continuous biomarkers exhibit clinically plausible distributions and ranges:

* Body mass index (BMI, kg/m²)
  * Mean (SD): 28.33 (5.03)
  * Median [IQR]: 28.33 [24.92, 31.73]
  * Range: 15.0–52.76
* Systolic blood pressure (SBP, mmHg)
  * Mean (SD): 123.31 (16.10)
  * Median [IQR]: 123.14 [112.39, 134.10]
  * Range: 55.85–187.79
* Estimated glomerular filtration rate (eGFR, mL/min/1.73 m²)
  * Mean (SD): 82.77 (6.09)
  * Median [IQR]: 82.94 [79.22, 86.66]
  * Range: 37.00–104.65
* Haemoglobin A1c (HbA1c, %)
  * Mean (SD): 4.79 (0.93)
  * Median [IQR]: 4.66 [4.24, 5.12]
  * Range: 2.23–12.71

---

## Cardiovascular Outcomes and Follow-up

Each individual is assigned a nominal 5-year follow-up period:
* Overall 5-year CVD event rate: 4.02%
* Mean follow-up time: 4.80 years

Event times are generated from a calibrated time-to-event model and administratively censored, producing realistic right-censoring patterns suitable for survival analysis.

---

## Intended Use

PRIME-CVD Data Asset 1 is intended to function as:

* a reference cohort for cardiovascular risk modelling exercises,
* a baseline comparator for reconstructed EMR-style datasets,
* and a transparent synthetic benchmark with known generative assumptions.

It is not designed to replace real clinical data, but to provide a stable, privacy-preserving substrate for method development, education, and reproducible demonstration.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-09)
