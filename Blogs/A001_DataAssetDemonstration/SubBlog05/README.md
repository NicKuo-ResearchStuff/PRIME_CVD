# PRIME-CVD Data Asset 1:</br>Designing a Simulated Cohort from Public Evidence</br>Example using Smoking Status Conditional on IRSD

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog07.png" width="600"/>

Hey, hello, and Kia Ora!

In [earlier posts](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A001_DataAssetDemonstration/SubBlog04), we introduced PRIME-CVD Data Asset 1 as a clean, analysis-ready cohort and documented what it looks like at baseline.</br>
In this post, we focus on the mentality behind PRIME-CVD’s design, what to watch out for when working with public sources like AIHW and ABS.

To make the design philosophy of PRIME-CVD concrete, this post presents one fully worked generative component from Data Asset 1:</br>
smoking status conditional on socioeconomic disadvantage (IRSD).

---

## Mathematical formulation

Let $S_i \in$ { $\text{non},\ \text{current},\ \text{ex}$ } </br>
denote the smoking status of individual $i$, and let </br>

$Q_i \in$ { $1,2,3,4,5$ } </br>

denote their assigned IRSD quintile, where $1$ corresponds to the most disadvantaged group.

Smoking is modelled as a categorical random variable conditionally distributed on IRSD:</br>

$S_i \mid Q_i = q \sim \text{Categorical}\left(p^{(q)}\_{\text{non}}, p^{(q)}\_{\text{current}}, p^{(q)}\_{\text{ex}}\right), \qquad q \in {1,\ldots,5}$

Each quintile $q$ is associated with a probability simplex </br>

$\mathbf{p}^{(q)} = \bigl( p^{(q)}\_{\text{non}}, p^{(q)}\_{\text{current}}, p^{(q)}\_{\text{ex}} \bigr), \quad \sum_k p^{(q)}_k = 1,$

with the defining qualitative constraint:</br>
current smoking prevalence decreases monotonically with socioeconomic advantage**.

Given a vector of IRSD assignments ${Q_i}_{i=1}^n$, smoking statuses are drawn independently within each quintile. This guarantees that the empirical conditional distribution </br>

$\mathbf{P}(S|Q)$

converges to the target distribution in expectation, while preserving individual-level variability.

---

## Hyperparameters: what is required, and where it comes from

This formulation requires a small, explicit set of hyperparameters.

### Required hyperparameters

1. Smoking state space:
   $\mathcal{S} = {\text{non},\ \text{current},\ \text{ex}}$

2. IRSD strata:
   $\mathcal{Q} = {1,2,3,4,5}$

3. Quintile-specific probability vectors"
   $\mathbf{p}^{(q)} \quad \text{for each } q \in \mathcal{Q}$
   
5. Random number generator:
   Used only to realise draws from the categorical distribution; it does not encode epidemiologic structure.

---

### What is anchored in AIHW / ABS sources

Public Australian sources (*e.g.,* AIHW National Drug Strategy Household Survey summaries, ABS socioeconomic reporting) directly support:

* the ordering of smoking prevalence across IRSD quintiles,
* the existence and direction of the socioeconomic gradient,
* the approximate proportion of non-smokers, current smokers, and ex-smokers at the population level.

These sources justify:

* conditioning smoking on IRSD,
* using three smoking categories,
* and enforcing monotonicity of current smoking with disadvantage.

---

### What remains a modelling choice

Public sources do not uniquely determine:

* the exact numeric probability triplet for each quintile,
* the smoothness of transitions between quintiles,
* or how ex-smokers are redistributed across strata.

Those quantities are therefore treated as transparent modelling assumptions, chosen to be:

* internally consistent,
* epidemiologically plausible,
* and stable under resampling.

They are published here explicitly so readers can inspect and critique them.

---

## Reference implementation

Below is the exact implementation used to generate smoking status in PRIME-CVD Data Asset 1.

```python
import numpy as np

SMOKING_STATES = np.array(["non", "current", "ex"])

SMOKING_PROB_MAP_IRSD = {
    1: {"non": 0.64,  "current": 0.16,  "ex": 0.20},
    2: {"non": 0.695, "current": 0.125, "ex": 0.18},
    3: {"non": 0.73,  "current": 0.10,  "ex": 0.17},
    4: {"non": 0.775, "current": 0.075, "ex": 0.15},
    5: {"non": 0.81,  "current": 0.05,  "ex": 0.14},
}

def sample_smoking_given_irsd(irsd_quintile, rng=None):
    """
    Sample smoking status conditional on IRSD quintile.

    Parameters
    ----------
    irsd_quintile : array-like of shape (n,)
        IRSD quintile for each individual (values 1–5).
    rng : numpy.random.Generator, optional
        Random number generator for reproducibility.

    Returns
    -------
    smoking_status : ndarray of shape (n,)
        Smoking status ("non", "current", or "ex") for each individual.
    """
    if rng is None:
        rng = np.random.default_rng()

    n = len(irsd_quintile)
    out = np.empty(n, dtype=object)

    for q in np.unique(irsd_quintile):
        idx = np.where(irsd_quintile == q)[0]
        if len(idx) == 0:
            continue

        p = SMOKING_PROB_MAP_IRSD[q]
        probs = np.array([p["non"], p["current"], p["ex"]])

        out[idx] = rng.choice(
            SMOKING_STATES,
            size=len(idx),
            p=probs
        )

    return out
```

This function is deterministic up to the supplied RNG and preserves
$\text{P}(\text{smoking} \mid \text{IRSD})$ exactly in expectation.

---

## Overall design mentality

This example illustrates the core PRIME-CVD philosophy:</br>
Public data justify gradients and causal structure -- not microscopic precision.

By encoding smoking as conditionally dependent on IRSD, and then allowing that dependence to propagate into downstream cardiometabolic outcomes, we preserve the causal narrative implied by public evidence.

---

Cheers,</br>
\- Nic

(Last edit: 2026-01-16)
