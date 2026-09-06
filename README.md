# Colonial Ties and the Shape of Global Migration

A gravity-model analysis of what best explains global migration corridors:
colonial history, economic pull, or geographic distance. Full methodology,
diagnostics, and the resulting articles are in this repository.

**Headline finding (Piece 1):** a shared colonial tie is associated with roughly
three times more migration between two countries than an otherwise
identical pair without one -- ahead of GDP, shared language, and distance.

**Headline finding (Piece 2):** UK outward emigration grew only 21% over 34 years
(3.85M → 4.67M), while inward migration more than tripled (+202%: 2.89M → 8.73M).
No visible break in either direction at 2016 (Brexit referendum) or 2020 (COVID).

---

## Published Articles

**Piece 1 — The Empire That Never Left**
Published on Medium — [Read here](https://medium.com/@mehmood.vc/the-empire-that-never-left-72cc1dc0b2ab)

**Piece 2 — Two Britains Revisited**
Published on Medium — [Read here](https://medium.com/@mehmood.vc/two-britains-revisited-314c3ecf071b)

*Piece 3 — coming soon*

---

## Key Findings

### Piece 1 — Global gravity model
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

### Piece 2 — UK outward migration and Brexit
- **Inward migration is the dominant story**: inward stock more than tripled
  (+202%) while outward grew only 21% over the same 34-year period
- **No Brexit break visible**: neither settler-destination nor EU-destination
  outward emigration shows a break at 2016 or 2020 — the deceleration
  in EU-destination emigration begins in 2010-2015, pre-referendum
- **Canada in long decline**: settler-destination aggregate is flat because
  Canada (-41% over 34 years) offsets Australia and USA stability
- **Poland spike is a measurement story**: 103x growth in UK-born Polish
  residents most plausibly reflects citizenship acquisition post-2004
  accession, not actual emigration of UK-born people
- **Colonial-tie inward migration**: 15 of the top 30 inward origins carry
  a former colonial tie — the single largest category ahead of EU origins
- **Data quality**: Malta, Bangladesh, Cyprus flagged for uniform-scaling
  artifact; Thailand's 2000-2005 jump confirmed as a destination-side
  discontinuity affecting all origins simultaneously

---

## Repository Structure

```
├── notebooks/
│   ├── 01.migration_gravity_model.ipynb                     # ETL pipeline: sources, merges, cleans the data
│   ├── 02.migration_gravity_analysis_piece1_final.ipynb     # Statistical analysis + Piece 1 visuals
│   └── 03_uk_emigration_piece2_final.ipynb                  # UK outward/inward migration + Piece 2 visuals
├── article/
│   └── README.md                                            # Published articles and series index
├── chart/                                                   # Generated visuals used in the articles
├── .gitignore
└── README.md
```

**Note:** the final merged dataset (`gravity_df.csv`, ~64MB) is not
tracked in this repository. It's fully and exactly reproducible by running
`01.migration_gravity_model.ipynb` against the three raw source files
below -- see **Reproducing the dataset**.

---

## Data Sources

Three raw inputs, none of them redistributed in this repo -- download
each directly:

| Source | What it provides | Link |
|---|---|---|
| World Bank development indicators | GDP, population, and economic data by country/year | [Global Socio-Economic & Demographic Insights — Kaggle](https://www.kaggle.com/datasets/samybaladram/databank-world-development-indicators) |
| UN DESA International Migrant Stock 2024 | Bilateral migration counts by country pair, 1990-2024 | [UN DESA](https://www.un.org/development/desa/pd/content/international-migrant-stock) — download the **"Destination and origin"** file specifically |
| CEPII GeoDist | Distance, shared border, language, and colonial-tie data by country pair | [CEPII](https://www.cepii.fr/CEPII/en/bdd_modele/bdd_modele_item.asp?id=6) — download the **`dist_cepii`** file |

---

## Reproducing the Dataset

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

---

## Running the Analysis

**Piece 1 analysis:**
Once `gravity_df.csv` exists, `02.migration_gravity_analysis_piece1_final.ipynb`
picks up from there -- PPML gravity regression, diagnostics (overdispersion,
multicollinearity, panel-clustering), the colonizer-group breakdown, and
all visuals used in Piece 1.

**Piece 2 analysis:**
`03_uk_emigration_piece2_final.ipynb` runs directly on `gravity_df.csv` --
UK outward and inward migration trends, data-quality checks (scaling artifact
test, Thailand discontinuity investigation, Poland spike cross-check),
settler/EU/rest-of-world breakdowns, and all visuals used in Piece 2.

---

## Key Methodological Decisions

Every non-obvious decision made in this project -- country-name
reconciliation, the country-categorization pass, PPML over log-linear
OLS, the panel-clustering fix, and each data-quality exclusion (UAE and
other Gulf states, Malaysia's frozen figures, Germany's reporting gaps,
Thailand's 2000-2005 discontinuity) -- is documented in full in the
published articles:

- Piece 1: [The Empire That Never Left](https://medium.com/@mehmood.vc/the-empire-that-never-left-72cc1dc0b2ab)
- Piece 2: [Two Britains Revisited](https://medium.com/@mehmood.vc/two-britains-revisited-314c3ecf071b)

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python · Pandas | Data wrangling and pipeline |
| statsmodels (PPML) | Gravity model regression, overdispersion diagnostics |
| pycountry | ISO3 country code crosswalk |
| Matplotlib | Visualisations |

---

## Series Plan

This repository will be updated as the series develops:

- **Piece 1** — Colonial ties and the shape of global migration *(published)*
- **Piece 2** — UK outward migration and Brexit *(published)*
- **Piece 3** — French colonial corridors: Algeria, Morocco, Senegal *(planned)*
- **Piece 4** — South Asian migration and the Gulf *(planned)*
- **Piece 5** — The FIFA connection: does migration gravity predict football diaspora? *(planned)*

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
- UK as destination has only 35 reported origin countries in this dataset
  (a genuine property of what the UN panel reports for GBR, not a
  filtering decision)

---

## Author

Mehmood Ahmed Khan — Data Scientist & Analytics Engineer, Karachi, Pakistan
GitHub: [github.com/Mehmoodkhans](https://github.com/Mehmoodkhans)
LinkedIn: [linkedin.com/in/mehmood](https://linkedin.com/in/mehmood)
Medium: [@mehmood.vc](https://medium.com/@mehmood.vc)
