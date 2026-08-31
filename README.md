# Colonial Ties and the Shape of Global Migration

A gravity-model analysis of what best explains global migration corridors:
colonial history, economic pull, or geographic distance. Full methodology,
diagnostics, and the resulting article are in this repository.

**Headline finding:** a shared colonial tie is associated with roughly
three times more migration between two countries than an otherwise
identical pair without one -- ahead of GDP, shared language, and distance.
See [`article/piece1_article_outline.md`](article/piece1_article_outline.md)
for the full writeup, and
[`article/project_handoff_v2.md`](article/project_handoff_v2.md) for the
complete methodology record.

## Published Articles

**Piece 1 — The Empire That Never Left**
Published on Medium — [Read here](https://medium.com/@mehmood.vc/the-empire-that-never-left-72cc1dc0b2ab)

*Piece 2 — coming soon*
---

## Key Findings

- **Colonial ties dominate**: a shared colonial history is associated
  with ~3x more migration than an otherwise identical country pair —
  the strongest effect in the model, ahead of GDP, shared language,
  and distance
- **Ottoman effect is a data signal, not history**: the Ottoman
  colonial coefficient collapsed near zero once Syria-Turkey was
  removed — capturing a modern refugee crisis, not a historical pattern
- **Commonwealth siblings**: former UK colonies show elevated migration
  with each other, independent of direct UK ties or shared language
- **Gulf states excluded**: UAE, Kuwait, Oman, Qatar, and Bahrain show
  near-identical growth ratios across every origin — a signature of
  estimated data, not independently measured bilateral figures
- **Saudi Arabia is South Asia's real destination**: the Gulf dominates
  South Asian migration corridors ahead of the UK, USA, and Australia

---

## Repository structure

```
├── notebooks/
│   ├── 01.migration_gravity_model.ipynb                    # ETL pipeline: sources, merges, cleans the data
│   └── 02.migration_gravity_analysis_piece1_final.ipynb    # Statistical analysis + Piece 1 visuals
├── article/
│   ├── piece1_article_outline.md                # The article itself
│   └── project_handoff_v2.md                    # Full methodology handoff document
├── chart/                                        # Generated visuals used in the article
├── .gitignore
└── README.md
```

**Note:** the final merged dataset (`gravity_df.csv`, ~64MB) is not
tracked in this repository. It's fully and exactly reproducible by running
`01.migration_gravity_model.ipynb` against the three raw source files
below -- see **Reproducing the dataset**.

---

## Data sources

Three raw inputs, none of them redistributed in this repo -- download
each directly:

| Source | What it provides | Link |
|---|---|---|
| World Bank development indicators | GDP, population, and economic data by country/year | [Global Socio-Economic & Demographic Insights — Kaggle](https://www.kaggle.com/datasets/samybaladram/databank-world-development-indicators) |
| UN DESA International Migrant Stock 2024 | Bilateral migration counts by country pair, 1990-2024 | https://www.un.org/development/desa/pd/content/international-migrant-stock -- download the **"Destination and origin"** file specifically |
| CEPII GeoDist | Distance, shared border, language, and colonial-tie data by country pair | https://www.cepii.fr/CEPII/en/bdd_modele/bdd_modele_item.asp?id=6 -- download the **`dist_cepii`** file |

## Reproducing the dataset

1. Download all three files linked above.
2. Place them in the same folder as `01.migration_gravity_model.ipynb`.
3. Rename the World Bank zip file to match exactly what the notebook
   expects (check the `CONFIG` cell near the top of the notebook for the
   current expected filename).
4. Run the notebook top to bottom. `gravity_df.csv` will be generated in
   the same folder.

This process is fully deterministic -- re-running it against the same
three source files always produces a byte-for-byte identical
`gravity_df.csv` (verified by direct checksum comparison during this
project's development).

## Running the analysis

Once `gravity_df.csv` exists, `02.migration_gravity_analysis_piece1_final.ipynb`
picks up from there -- PPML gravity regression, diagnostics (overdispersion,
multicollinearity, panel-clustering), the colonizer-group breakdown, and
all Part 1/Part 2 visuals used in the article.

## Key methodological decisions

Every non-obvious decision made in this project -- country-name
reconciliation, the country-categorization pass, PPML over log-linear
OLS, the panel-clustering fix, and each data-quality exclusion (UAE and
other Gulf states, Malaysia's frozen figures, Germany's reporting gaps)
-- is documented in full in
[`article/project_handoff_v2.md`](article/project_handoff_v2.md).

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python · Pandas | Data wrangling and pipeline |
| statsmodels (PPML) | Gravity model regression, overdispersion diagnostics |
| pycountry | ISO3 country code crosswalk |
| Matplotlib | Visualisations |

---

## This is Part 1 of a series

This repository will be updated as the series develops:

- **Piece 1** — Colonial ties and the shape of global migration *(this piece)*
- **Piece 2** — UK outward migration and Brexit *(in progress)*
- **Piece 3** — French colonial corridors: Algeria, Morocco, Senegal *(planned)*
- **Piece 4** — South Asian migration and the Gulf *(planned)*
- **Piece 5** — The FIFA connection: does migration gravity predict
  football diaspora? *(planned)*

---

## Limitations

- Gulf state bilateral figures (UAE, Kuwait, Oman, Qatar, Bahrain)
  excluded due to estimated/proportional data signatures
- Malaysia partially flagged — identical figures repeated across
  2015/2020/2024 snapshots for 7 of 26 origins
- Distance data missing for ~5 successor states (~1.6% of migrant volume)
- Country-of-birth measure used throughout — not citizenship or legal
  nationality, which matters for Brexit analysis in Piece 2
- Panel structure covers 1990–2024 but UN snapshots are 5-year intervals,
  not annual

---

## Author

Mehmood Ahmed Khan — Data Scientist & Analytics Engineer, Karachi, Pakistan
GitHub: [github.com/Mehmoodkhans](https://github.com/Mehmoodkhans)
LinkedIn: [linkedin.com/in/mehmoood](https://linkedin.com/in/mehmoood)
Medium: [@mehmood.vc](https://medium.com/@mehmood.vc)
