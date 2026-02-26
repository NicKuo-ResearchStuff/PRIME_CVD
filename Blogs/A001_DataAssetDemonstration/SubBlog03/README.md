# PRIME-CVD Data Asset 2:</br> A Relational EMR-Style Dataset for Teaching</br> Data Cleaning and Reconstruction

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog04.png" width="600"/>

Hey, hello, and Kia Ora!

In this post, we introduce PRIME-CVD Data Asset 2, a relational, EMR-style transformation of the clean DAG-generated cohort presented in [Data Asset 1](https://github.com/NicKuo-ResearchStuff/Synthetic_Data_Related_Project_Staging/tree/main/chaptY/Blog001).

Unlike the clean, one-row-per-patient structure used for modelling, Data Asset 2 is deliberately fragmented and degraded. It is designed to reproduce the structural, lexical, and temporal challenges of working with routinely collected electronic medical records (EMR), while remaining fully synthetic and safe for classroom use.

This post documents how the dataset is structured and what students are expected to reconstruct before any modelling can begin.

---

## From Clean Cohort to EMR Tables

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog04_Fig01.png" width="800"/>

All individuals, covariates, and outcomes are retained from Data Asset 1 -- but they are divided across multiple tables and distorted by realistic EMR artefacts. This mirrors common primary-care and hospital database architectures, where identifiers, diagnoses, and measurements reside in separate systems and must be re-linked for analysis.

Data Asset 2 helps students to understand: “Why is real EMR data never analysis-ready?”

---

## Relational Table Structure

PRIME-CVD Data Asset 2 consists of three linked CSV tables, collectively referred to as `PatientEMR`.

### 1. PatientMasterSummary

This table provides the patient index and outcome anchor.

Each row corresponds to one individual and contains:

* a simulated, non-sequential patient identifier,
* age recorded as Age at 2024,
* IRSD quintile,
* smoking status (with injected missingness),
* a binary CVD event indicator,
* and a coarsened year–month outcome or censoring date.

A preview of the first few rows illustrates the structure:

| Patient_ID | Age_At_2024 | Smoking | IRSD | CVD_Event | CVD_Time |
| ---------: | ----------: | ------- | ---: | --------: | -------- |
|        269 |       57.40 | non     |    4 |         1 | 2019-12  |
|        272 |       46.23 | ex      |    3 |         0 | 2022-12  |
|        281 |       62.49 | non     |    5 |         0 | 2022-12  |

This table resembles a typical EMR extract summary: useful, but insufficient on its own for modelling.

---

### 2. PatientChronicDiseases

This table expands baseline chronic conditions into a presence-only diagnosis list.

Each row represents one recorded condition for one patient, using:

* heterogeneous free-text labels,
* ICD-like codes

For example:

| Patient_ID | Category   | Date    |
| ---------: | ---------- | ------- |
| 1338163469 | Diabetes   | 2012-05 |
|  545940569 | ICD10: E11 | 2016-10 |
| 7134075944 | Diabetes   | 2013-02 |

There is no single canonical diabetes column here.
Students must decide how to recognise, harmonise, and collapse diagnoses into usable indicators.

---

### 3. PatientMeasAndPath

This table stores biomarkers and vital signs in long format, as is typical for pathology and observation systems.

Each patient appears multiple times -- once per measurement -- with:

* varied string descriptions,
* mixed units

Example rows:

| Patient_ID | Value  | Description | Date    | Unit |
| ---------: | -----: | ----------- | ------- | ---- |
| 5790852944 | 4.50   | HBA1C       | 2013-02 | %    |
| 3141314912 | 4.16   | Hb A1c      | 2016-09 | %    |
| 3311104121 | 131.55 | SBP         | 2013-11 | mmHg |

This structure forces students to confront:

* long-to-wide reshaping,
* unit harmonisation,
* and string-based variable identification.

---

## Injected EMR Artefacts

Data Asset 2 is intentionally not messy by accident.

We inject controlled artefacts that mirror those encountered in real EMR systems:

* ID scrambling:</br>
  Patient identifiers are non-sequential and opaque, but deterministic.

* Shifted age reference:</br>
  Age is recorded relative to an extraction year, not baseline.

* Patterned missingness:</br>
  Smoking status is selectively missing among non-smokers.

* Lexical heterogeneity:</br>
  Diagnoses and measurements appear under multiple synonymous labels.

* Unit inconsistency:</br>
  A subset of HbA1c values is recorded in mmol/mol instead of %.

These artefacts are documented quantitatively in the manuscript appendix, but here they serve a single pedagogic purpose:</br>
to make reconstruction necessary rather than optional.

---

## Teaching Philosophy

PRIME-CVD Data Asset 2 exists to teach:

* data cleaning,
* linkage and harmonisation,
* bias from missingness,
* and the cost of EMR design decisions.

Only after students reconstruct a cohort resembling Data Asset 1 do they proceed to modelling -- completing the full lifecycle from messy EMR to interpretable risk estimates.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-13)
