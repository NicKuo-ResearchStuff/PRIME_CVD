# Viz 01</br>when risk space has shape

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog20_Viz1.png" width="600"/>

Hey, hello, and Kia Ora!

In this blog, we question: What does healthcare data look like before we model it?

---

## Before Modelling, There Is Geometry

Most risk-modelling papers start here:

* fit Cox,
* compute C-index,
* maybe calibration,
* maybe NRI.

But, every patient is a vector representation:

* age,
* smoking,
* diabetes,
* kidney function,
* blood pressure,
* socioeconomic context.

So when we talk about “risk”, we are really talking about:</br>
how the high-dimensional space is structured.

Do patients form natural groups?</br>
Are there smooth gradients?</br>
Are some phenotypes clearly separated?</br>

---

## Why Visualisation Matters in Healthcare

Healthcare data are not just large — they are heterogeneous.

Two patients with the same predicted 5-year risk may arrive there through:

* different combinations of comorbidities,
* different behavioural patterns,
* different socioeconomic exposures.

If we only look at a risk score, we collapse that structure.

Visualisation helps us see:

* latent phenotypes,
* behavioural clusters,
* multimorbidity islands,
* continuous demographic gradients.

---

## t-SNE

[t-SNE (t-distributed Stochastic Neighbour Embedding)](https://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf) is a non-linear dimensionality reduction method.

In plain language:

It tries to place patients close together in 2D if they were close together in high-dimensional space.

It tries to preserve neighbourhoods, seeking to answer:</br>
Who lives near whom in risk space?

t-SNE is particularly good at revealing discrete phenotype.

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog20_Viz1_Fig01.png" width="600"/>

---

## Why This Matters for Modelling

If the data geometry is cluster-driven, then:

* sparse models may behave differently from full models,
* reclassification metrics may shift particular phenotypes (for combinations of features),
* calibration may vary across geometric regions.

It is hence worth asking:</br>
What does the risk landscape actually look like?

We will implement it in the next blog.

---

Cheers,</br>
\- Nic

(Last edit: 2026-03-06)
