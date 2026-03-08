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
See [here](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/2026_02_25_PrimeCvd_QuickStart.ipynb) to start using the PRIME-CVD data assets in Python.</br>
See [here](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/2026_02_25_PrimeCvd_QuickStart(R_Version).ipynb) to start using the PRIME-CVD data assets in R.

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

<!-- Side-by-side layout: text and illustration -->

<table>
<tr>
<td width="60%">

**[Series 01](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A001_DataAssetDemonstration) — The Dataset Itself**

* What it shows:</br>how the clean cohort is structured and how the EMR version is derived.
* Where it comes from:</br>a hand-specified causal DAG parameterised with ABS and AIHW evidence.
* Why it exists:</br>to demonstrate data provenance, causal assumptions, and realistic population structure.

</td>
<td width="40%">
  <img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_FrontPage_DataItself.png" alt="Series 01 Overview" width="400"/>
</td>
</tr>
</table>

---

<!-- Side-by-side layout: text and illustration -->

<table>
<tr>
<td width="60%">

**Teaching with PRIME-CVD**

* For educators:</br>
  **[Series 02](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A002_EducationFocus)** focuses on assessment design, showing how PRIME-CVD supports structured assignments and exams — from socioeconomic stratification tasks to Cox baseline interpretation and EMR reconstruction exercises. It demonstrates how the dataset enables fair, reproducible, and judgement-based evaluation rather than rote modelling.

* For students:</br>
  Below, we introduce core concepts in medical informatics through focused thematic series:
  * **Discrimination ([Series 03](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A003_DiscriminationBlogs)):**</br> how models rank individuals in risk space.
  * **Calibration ([Series 04](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A004_CalibrationBlogs)):**</br> how predicted risks relate to observed outcomes.
  * **Transportability ([Series 05](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A005_InternalExternalValidation)):**</br> how models behave across different populations.
  * **Deployability ([Series 06](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A006_ToLassoOrNotToLasso)):**</br> the trade-off between modelling richness and real-world feasibility.
  * **Risk Geometry ([Series 07](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A007_TsneAndVisualisation)):**</br> how patients cluster and form gradients in high-dimensional risk space.

</td>
<td width="40%">
  <img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_FrontPage_TeachSeries.png" alt="Teaching with PRIME-CVD" width="400"/>
</td>
</tr>
</table>

---

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
4. Kuo (2026). PRIME-CVD Data Asset 1: DAG-Simulated Cardiovascular Risk Cohort for Medical Informatics Education. figshare. Dataset. https://doi.org/10.6084/m9.figshare.31395765.v1
5. Kuo (2026). PRIME-CVD Data Asset 2: Relational EMR-Style Cardiovascular Dataset for Medical Informatics Education. figshare. Dataset. https://doi.org/10.6084/m9.figshare.31403028.v1

(Last edit: 2026-03-09)
