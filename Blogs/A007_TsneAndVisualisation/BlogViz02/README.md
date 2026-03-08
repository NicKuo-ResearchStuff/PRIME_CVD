# Viz 02</br>implementing t-SNE and reading the colours

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog21_Viz2.png" width="600"/>

Hey, hello, and Kia Ora!

Last time in [Viz 01](https://github.com/NicKuo-ResearchStuff/Synthetic_Data_Related_Project_Staging/tree/main/chaptY/BlogViz01), we asked:</br>
What does the risk landscape look like before we model it?

Today we do the promised thing:
* implement t-SNE (cleanly),
* explain the few choices that actually matter,
* and interpret what “colouring the same embedding” is telling us.

(Full runnable details are in the script in the same folder as this blog.)

---

## Step 1 — Don’t leak the outcome

We are exploring covariate geometry, not prediction.

So we drop the survival outcome fields:

```python
outcome_cols = ["cvd_event", "cvd_time"]
X_df = df_raw.drop(columns=outcome_cols)
```

If you keep them in, the embedding starts to reflect outcome separation, not phenotype structure.

---

## Step 2 — Numeric, scaled, and stable

t-SNE uses distances, so we need a numeric design matrix.

Smoking becomes one-hot:

```python
X_df = pd.get_dummies(X_df, columns=["smoking_status"], drop_first=False)
```

Then we standardise:

```python
X = StandardScaler().fit_transform(X_df.values)
```

---

## Step 3 — PCA before t-SNE

We do PCA first:

```python
X_pca = PCA(n_components=min(30, X.shape[1]), random_state=42).fit_transform(X)
```

This is a useful optional step that:
* reduces noise,
* speeds up t-SNE,
* improves stability.

For more about PCA vs t-SNE, consider reading [this blog](https://towardsdatascience.com/how-t-sne-outperforms-pca-in-dimensionality-reduction-7a3975e8cbdb/).

---

## Step 4 — Subsample and embed

t-SNE is expensive, so we sample:

```python
idx = rng.choice(X_pca.shape[0], size=10000, replace=False)
Z = TSNE(
    n_components=2,
    perplexity=30,
    init="pca",
    learning_rate="auto",
    random_state=42,
    n_iter=1500,
).fit_transform(X_pca[idx])
```

Perplexity (~30) sets the effective neighbourhood size: local structure matters more than global distances.

---

## One embedding, many lenses

Now the key move:

We compute one embedding `Z`, and recolour it by different covariates.

Recolouring the same `Z` keeps the terrain fixed and changes only the “overlay”.

---

## Diabetes vs Age: same islands, different stories

<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog21_Viz2_Fig01.png" width="600"/>
<img src="https://github.com/NicKuo-ResearchStuff/PRIME_CVD/blob/main/Supporting_Images/ZFig_PRIME_CVD_Blog21_Viz2_Fig02.png" width="600"/>


### Similarity: the islands sit in the same places

Because the coordinates `Z` are identical.

Colouring does not move points — it only reveals what variables align with the existing neighbourhood structure.

So the island layout reflects overall multivariate similarity across the whole risk-factor set.

### Difference: diabetes makes colour-pure islands, age does not

On the diabetes plot, one island is almost entirely red.</br>
That tells you diabetes behaves like a cluster-forming phenotype:</br>
people with diabetes share a tight multivariate signature (HbA1c and correlated cardiometabolic features),</br>
so they become neighbours and form a coherent region.

On the age plot, each island contains a spectrum of colours.</br>
That tells you age behaves like a gradient variable:</br>
it shifts people within phenotypic regions rather than splitting the space into separate age-defined groups.

---

Cheers,</br>
\- Nic

(Last edit: 2026-03-06)
