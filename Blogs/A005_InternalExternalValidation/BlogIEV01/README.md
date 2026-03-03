# Internal-External Validation Blog 01</br>when calibration leaves home

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog15_IEV1.png" width="600"/>

Hey, hello, and Kia Ora!

In the previous calibration posts, we stayed at home, meaning we kept:
* the same PRIME-CVD cohort,
* the same Cox model,
* the same predicted risks $\hat r_i(t)$,

and asked:</br>
Are the probabilities numerically honest?

Now we change the environment:
* From: Is the model calibrated in this population?
* To: Is the model calibrated when the population changes? (does it travel...?)

---

## About Population Change...

To clarify, we are not interested in testing calibration under a random split like:

* 80% train / 20% test.

Instead, we conduct structural tests, where:

* Train on IRSD 2–5, test on IRSD 1.
* Train on IRSD 1,3–5, test on IRSD 2.
* …
* Repeat for all strata.

Each socioeconomic quintile becomes its own deployment environment.

This tests transportability.

---

## What This Is Not

This setup is not about evaluating the goodness-of-fit of one all-knowing model.

It is not:</br>
“Train one grand model on everything and prove it works.”
* It is not the foundational-model philosophy.
* It is not a digital twin aspiration.
* It is not the claim that a single, globally trained model captures the entire structure of reality.

Instead, it is something more modest — and more disciplined.

---

## What This Is

This setup is about testing a hypothesis of robustness.

We hold the modelling backbone constant:

* same Cox architecture,
* same feature set (without IRSD),
* same calibration metric,
* same evaluation time horizon $t$.

What changes is the environment the backbone is exposed to during training.

Each leave-one-IRSD-out experiment asks:</br>
If this modelling idea were trained under slightly different circumstances,</br>
how fragile would it be when confronted with a population it has never seen?

This is not about perfection.

It is about stress-testing.

---

## Development vs Deployment

In practice, the final deployed model will almost certainly use training data from all IRSD strata.

But during development, we intentionally withhold structure to probe limits.

Why?

Because robustness is not proven by training on everything.

Robustness is revealed when structure is removed.

If the backbone architecture:
* remains calibrated,
* maintains small $D_{21}(t)$,
* and does not collapse under environmental variation,

**then we gain confidence that the modelling concept is stable.**

If calibration drifts sharply in a held-out IRSD stratum, that tells us something fundamental:

The modelling assumptions are environment-sensitive.

---

Cheers,</br>
\- Nic

(Last edit: 2026-02-19)
