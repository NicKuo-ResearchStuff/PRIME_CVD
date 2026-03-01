# PRIME-CVD Data Asset 1</br> Where Did This Dataset Come From?

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog05.png" width="600"/>

Hey, hello, and Kia Ora!

In the previous posts (see [this](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A001_DataAssetDemonstration/SubBlog01) and [this](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A001_DataAssetDemonstration/SubBlog02)), we introduced PRIME-CVD Data Asset 1 as a clean, analysis-ready cohort and documented its baseline characteristics.
In this post, we step back and answer a different question:</br>
Where did this dataset actually come from?

This post explains what we chose to encode, and why those decisions matter for teaching.

---

## A Design Constraint from the Start

PRIME-CVD Data Asset 1 was designed under three non-negotiable constraints:

1. No patient-level data</br>
   No EMR extracts, no registries, no training on real trajectories.

2. Only openly available sources</br>
   Government statistics, surveillance summaries, and published epidemiologic estimates.

3. Pedagogic sufficiency, not maximal realism</br>
   The dataset must be good enough to teach reasoning, not to mirror every nuance of reality.

This immediately rules out many popular approaches to “synthetic EMR”,</br>
*i.e., data generated using AI/ML techniques which learn directly from real patient data,</br>*
and forces a different design philosophy.

---

## Encoded Causal Relationships and Public Evidence
<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog05_Fig01.png" width="800"/>
PRIME-CVD Data Asset 1 is generated from a hand-specified causal DAG. Each edge below is supported by openly available population statistics or epidemiologic literature.

| **Parent → Child**   |                                    **What is being encoded** | **Primary open sources**                                                                                                                                                                                                                                               |
| -------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IRSD → Smoking**   | Smoking prevalence increases with socioeconomic disadvantage | [AIHW – Smoking (NDSHS)](https://www.aihw.gov.au/reports/smoking/tobacco-smoking-ndshs)</br>[Tobacco in Australia](https://www.tobaccoinaustralia.org.au/chapter-1-prevalence/1-7-trends-in-the-prevalence-of-smoking-by-socioec)                                        |
| **IRSD → BMI**       |        Higher deprivation associated with higher average BMI | [AIHW – Overweight & Obesity](https://www.aihw.gov.au/getmedia/3b5e2302-15d2-411f-8867-b5a50867e87c/overweight-and-obesity.pdf)</br>[AIHW – Inequalities](https://www.aihw.gov.au/reports/overweight-obesity/inequalities-overweight-social-determinants-health/summary) |
| **BMI → Diabetes**   |                              Obesity increases diabetes risk | [NHMRC Obesity Guidelines](https://www.nhmrc.gov.au/sites/default/files/documents/reports/clinical%20guidelines/n57a-obesity-systematic-review.pdf)</br>[Obesity Evidence Hub](https://www.obesityevidencehub.org.au/collections/impacts/health-impacts-of-obesity)      |
| **BMI → CKD**        |                            Obesity mildly increases CKD risk | [AIHW – CKD Facts](https://www.aihw.gov.au/reports/chronic-kidney-disease/chronic-kidney-disease/contents/how-many-people-are-living-with-ckd)</br>[Nawaz et al. 2023](https://onlinelibrary.wiley.com/doi/10.1002/osp4.629)                                             |
| **BMI → SBP**        |                   Adiposity elevates systolic blood pressure | [NHMRC Obesity Review](https://www.nhmrc.gov.au/sites/default/files/documents/reports/clinical%20guidelines/n57a-obesity-systematic-review.pdf)                                                                                                                        |
| **Age → Diabetes**   |                       Diabetes prevalence increases with age | [AIHW – Diabetes Facts](https://www.aihw.gov.au/reports/diabetes/diabetes/contents/how-common-is-diabetes/all-diabetes)</br>[ABS – Diabetes](https://www.abs.gov.au/statistics/health/health-conditions-and-risks/diabetes/latest-release)                               |
| **Age → CKD**        |                            CKD prevalence increases with age | [AIHW – CKD Facts](https://www.aihw.gov.au/reports/chronic-kidney-disease/chronic-kidney-disease/contents/how-many-people-are-living-with-ckd)</br>[RACGP – CKD in the elderly](https://www.racgp.org.au/afp/2012/december/ckd-in-the-elderly)        |
| **Age → SBP**        |                                Blood pressure rises with age | [AIHW – High BP](https://www.aihw.gov.au/reports/risk-factors/high-blood-pressure/contents/summary)</br>[ABS – Hypertension](https://www.abs.gov.au/statistics/health/health-conditions-and-risks/hypertension-and-high-measured-blood-pressure/latest-release)          |
| **Age → eGFR**       |                            Kidney function declines with age | [AIHW – CKD Facts](https://www.aihw.gov.au/reports/chronic-kidney-disease/chronic-kidney-disease/contents/how-many-people-are-living-with-ckd)                                                                                                                         |
| **Age → AF**         |                              AF incidence increases with age | [AIHW – AF Facts](https://www.aihw.gov.au/reports/heart-stroke-vascular-diseases/hsvd-facts/contents/all-heart-stroke-and-vascular-disease/atrial-fibrillation)</br>[MORGAM consortium](https://pubmed.ncbi.nlm.nih.gov/34341095/)                               |
| **Diabetes → HbA1c** |                                  Diabetes elevates glycaemia | [RACGP – HbA1c](https://www1.racgp.org.au/ajgp/2021/september/more-than-just-a-number)</br>[ADA – A1C](https://diabetes.org/about-diabetes/a1c)                                                                                                                          |
| **Diabetes → CKD**   |                    Diabetes substantially increases CKD risk | [Kim et al. 2023 (JAHA)](https://www.ahajournals.org/doi/10.1161/JAHA.122.028496)                                                                                                                                                                                      |
| **Diabetes → SBP**   |                          Diabetes associated with higher SBP | [Liu et al. 2025 (World J Diabetes)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12278073/)                                                                                                                                                                     |
| **CKD → eGFR**       |                          CKD markedly lowers filtration rate | [Marx-Schütt et al. 2025 (Eur Heart J)](https://pubmed.ncbi.nlm.nih.gov/40196891/)                                                                                                                                                                 |
| **CKD → SBP**        |                                  CKD elevates blood pressure | [Georgianos & Agarwal 2023 (NDT)](https://pubmed.ncbi.nlm.nih.gov/37355779/)                                                                                                                                                                             |
| **CKD → AF**         |                                        CKD increases AF risk | [Gadde et al. 2022 (Cureus)](https://pubmed.ncbi.nlm.nih.gov/36106212/)                                                                                                                                                                              |
| **Smoking → CKD**    |                                   Smoking increases CKD risk | [Xia et al. 2017 (NDT)](https://pubmed.ncbi.nlm.nih.gov/28339863/)                                                                                                                                                                                         |
| **Smoking → SBP**    |                                Smoking slightly elevates SBP | [AIHW – Biomedical Risk Factors](https://www.aihw.gov.au/reports/australias-health/biomedical-risk-factors)                                                                                                                                                            |
| **Smoking → AF**     |                                    Smoking increases AF risk | [Aune et al. 2018 (Eur J Prev Cardiol)](https://pubmed.ncbi.nlm.nih.gov/29996680/)                                                                                                                                                                    |

### Key Australian organisations

| **Abbreviation** | **Full name**                                |
| ---------------- | -------------------------------------------- |
| **AIHW**         | Australian Institute of Health and Welfare   |
| **ABS**          | Australian Bureau of Statistics              |
| **NHMRC**        | National Health and Medical Research Council |
| **RACGP**                                             | Royal Australian College of General Practitioners                      |

---

## The Minimal Desiderata We Enforced

When designing Data Asset 1, we asked a small number of concrete questions.
1. Can students recognise the population?
2. Do stratifications reveal structure?
3. Do models behave sensibly?

If a feature did not support at least one of these goals, it was excluded.

---

## Closing Notes

PRIME-CVD Data Asset 1 is not a replica of reality.

It is a distillation:

* of what we know publicly,
* of what we can justify pedagogically,
* and of what students must understand before they confront real EMR data.

---

Cheers,<br>
\- Nic

(Last edit: 2026-01-14)
