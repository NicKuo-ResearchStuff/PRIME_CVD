# Internal-External Validation Blog 02</br>implementing an experiment

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog16_IEV2.png" width="600"/>

Hey, hello, and Kia Ora!

In the [previous post](https://github.com/NicKuo-ResearchStuff/PRIME_CVD/tree/main/Blogs/A005_InternalExternalValidation/BlogIEV01), we introduced the idea of internal–external validation.

Today, let us try to implement it.

---

## What Is the Environment?

Let us choose `IRSD_quintile` as the key structural variable.</br>
We will not feed it as a predictor to the model, and instead </br>
use it to define the environment.

Each quintile becomes:
* a potential training world, or
* a deployment world.

---

## What Remains Fixed

Across all experiments, we hold the following constant:
* Model architecture -- Cox proportional hazards (`CoxPHFitter`)
* Model hyperparameter -- Penalisation strength (`penalizer = 0.05`)
* Experimental hyperparameter
* * Experimental Evaluation horizon (`t = 4.88`)
* * Risk binning (`K = 20`)
* Evaluation setup
* * Calibration slope through origin
* * Deviation metric ( D_{21}(t) = |1 - a| )

As you can see, the only thing that changed is the training environment.

---

## Two Experiments

We ran two structured evaluations.

### Baseline

Where we
* Train on all IRSD strata
* Then evaluate calibration within each quintile

This tells us:</br>
If the model sees everything during training, how calibrated is it inside each environment?

The output looks like:

```
IRSD  a_baseline  D21_baseline
1     1.167       0.167
2     1.255       0.255
3     1.221       0.221
4     1.167       0.167
5     1.111       0.111
```

### Leave-One-IRSD-Out (Internal–External Validation)

Now we remove one quintile from training.

For each quintile $q$:
* Train on IRSD ≠ $q$
* Test only on IRSD = $q$

This simulates deployment into a population the model has never seen during fitting.

Results:

```
IRSD  a_loo   D21_loo
1     1.163   0.163
2     1.274   0.274
3     1.238   0.238
4     1.162   0.162
5     1.088   0.088
```

## Comapring Results

For most quintiles, Baseline and LOO slopes are similar.</br>
Hence removing one socioeconomic stratum during training</br>
does not dramatically destabilise calibration</br>
when evaluated inside that stratum.

This suggests structural stability.

However, we also find that</br>
quintiles 2 and 3 show slightly larger deviations under LOO.</br>
Telling us that</br>
Those environments may contain patterns</br>
that are not fully reconstructed</br>
from the remaining strata.

---

## Why This Matters

If baseline calibration is acceptable but LOO collapses,</br>
then the model relies on environment-specific structure.

If both are similar,</br>
then the modelling backbone is robust.

Here, the modelling decision</br>
(both the choice of backbone architecture and the non-environmental hyperparameter choices)</br> 
appears reasonably stable.</br>
There is thus robustness under perturbation.

---

## Reproducibility

The full Python script used for this experiment is attached in the same folder as this blog post.

Why not try the code youself, and test to see if you can modify the code to implement</br>
the leave-one-Age Group-out internal-external validation?

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-20)
