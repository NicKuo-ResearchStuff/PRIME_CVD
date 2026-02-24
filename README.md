<!-- Logo and Branding -->

<p align="left">
  <img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Logo_ReDo.png" alt="PRIME-CVD Logo" width="600"/>
</p>

---

# About PRIME‑CVD

PRIME‑CVD (Parametrically Rendered Informatics Medical Environment for Cardiovascular Disease)</br>
is an educational, privacy-preserving simulated dataset and teaching environment developed by the Centre for Big Data Research in Health (CBDRH), UNSW. PRIME‑CVD provides fully parameterised, DAG-driven simulated data designed specifically for teaching causal reasoning, EMR cleaning, and cardiovascular risk modelling without exposing real patient records.

* What it provides:
  * two complementary data assets (a clean cohort and an EMR-style relational transform),
  * worked notebooks (survival analysis, causal-sensitivity experiments, ... *etc*), and
  * reproducible code for cohort assembly and harmonisation.
* How it’s built:
  * variables are generated deterministically from a hand-specified causal DAG
  * parameterised using public Australian statistics (ABS, AIHW) and
  * published epidemiologic estimates.
* Datasets included:
  * <ins>Data Asset 1</ins>: Clean, analysis-ready cohort
    * 50,000 simulated adults
    * IRSD quintile, age, smoking, BMI, diabetes, CKD, HbA1c, eGFR, SBP, AF, cvd event indicator, time to cvd event
  * <ins>Data Asset 2</ins>: Relational EMR-style tables with injected heterogeneity, missingness, and unit inconsistencies
    * PatientMasterSummary
    * PatientChronicDiseases
    * PatientMeasAndPath

**Why it’s safe**</br>
All records are generated de novo from aggregate priors; no patient-level EMR is used, minimising disclosure risk.</br>
**Who it’s for**</br>
Educators and students learning data cleaning, causal inference, bias analysis, and survival modelling; researchers testing causal discovery.

---
See [here](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/2026_02_25_PrimeCvd_QuickStart.ipynb) to start using the PRIME-CVD data assets.

---

<!-- Side-by-side layout: text and illustration -->

<table>
<tr>
<td width="60%">

**Highlights of PRIME‑CVD**

* Open-access:</br>dataset CSVs, code, and instructional notebooks.
* Designed for teaching:</br>clear separation between the data-generating DAG and the observation process (EMR artefacts).
* Reproducible:</br>deterministic pipelines to regenerate cohorts at arbitrary scale.
* Two assets:</br>ideal cohort for modelling and messy EMR for data-engineering exercises.

</td>
<td width="40%">
  <img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_FrontPage_Highlights.png" alt="PRIME‑CVD Overview" width="400"/>
</td>
</tr>
</table>

---
<p align="left">
  <img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_FrontPage_WIP.png" alt="PRIME-CVD Logo" width="600"/>
</p>

Nic is still working on this repository... :)

---

# Team
* [Dr. Nic Kuo (CBDRH, UNSW)](https://www.unsw.edu.au/staff/nic-kuo)
* [Dr. Marzia Hoque (CBDRH, UNSW)](https://www.unsw.edu.au/staff/marzia-hoque-tania)
* [Prof. Blanca Gallego (CBDRH, UNSW)](https://www.unsw.edu.au/staff/blanca-gallego-luxan)
* [Prof. Louisa Jorm (CBDRH, UNSW)](https://www.unsw.edu.au/staff/louisa-jorm)

For questions or collaboration: Nic Kuo — [n.kuo@unsw.edu.au](mailto:n.kuo@unsw.edu.au)

---

# References & Further Reading

1. PRIME-CVD manuscript not yet archived...
2. Australian Bureau of Statistics (ABS) sources therein [1].
3. Australian Institute of Health and Welfare (AIHW) sources therein [1].

(Last edit: 2026-02-25)
