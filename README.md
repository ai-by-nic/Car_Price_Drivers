# What Drives the Price of a Used Car? — Practical Application 2

This repository contains my analysis for **UC Berkeley ML/AI – Practical Application 2** on used‑car pricing.  
The goal: **identify the factors that most influence price** and provide dealer‑friendly guidance for stocking and pricing.

> 📒 Open the analysis notebook: **[nic_r-practical_application-2.ipynb](./nic_r-practical_application-2.ipynb)**

---

## Summary of Findings (dealer‑friendly)

- **Age & mileage dominate.** On average, price changes by about **−\$720 per additional year** and **−\$85 per +1,000 miles**.
- **Title & condition matter.** Clean titles and better conditions command clear premiums; **salvage/rebuilt** require steep discounts.
- **Segment effects exist.** Trucks/SUVs and **4WD** often price higher in most markets; adjust to local demand.
- **Complete listings sell better.** Title status, mileage, condition, VIN and clear photos are consistently associated with stronger pricing.

**Quick Pricing Rule of Thumb**  
_Target = Comp − ( \$720 × Δyears ) − ( \$85 × Δmiles/1,000 ) + TitleAdj + ConditionAdj + FeatureAdj._

---

## Data & Methods (brief)

- Dataset: public used‑vehicle listings (subsample of ~100k rows after cleaning/dedup/winsorizing).
- Prep: VIN dedupe, drop non‑positive prices, winsorize price (1–99%), range filters for year/odometer, engineer `car_age`, collapse rare categories, impute + scale + one‑hot.
- Models compared: **OLS**, **Ridge (L2)**, **Lasso (L1)** with **5‑fold cross‑validation**.
- Metric: **MAE** primary; **RMSE** and **R²** reported.

---

## Model Performance

| Metric   | CV Best (Lasso) | Hold‑out (20%) | Baseline (median price) |
| -------- | --------------: | -------------: | ----------------------: |
| **MAE**  |    ≈ **$5,597** |     **$5,648** |              **$9,824** |
| **RMSE** |               — |     **$8,351** |                       — |
| **R²**   |               — |       **0.58** |                       — |

> Note: Lasso had the lowest CV MAE, but the gap to Ridge/OLS was only ~**\$4** (CV SD ~**\$27**) → a **practical tie**. Either model yields similar accuracy; Lasso was selected for its light feature selection.

---

## How to Use (for dealers)

- **Stocking:** favor **newer, low‑mile, clean‑title** vehicles in segments that turn fast locally.
- **Pricing:** start from **local comps**; apply the **age/mileage** adjustments and your house adds/deducts for title/condition/features.
- **Monitor:** check average miss monthly; if it drifts, tune the add/deduct numbers.

See the **Deployment — Dealer One‑Pager** section inside the notebook for a concise playbook.

---

## Repository Contents

- `nic_r-practical_application-2.ipynb` — full CRISP‑DM analysis notebook (EDA → Prep → Modeling → Evaluation → Deployment).

---

## Acknowledgments

Course: **UC Berkeley ML/AI (Emeritus)** — Practical Application 2. Models built with Python, pandas, scikit‑learn, seaborn/matplotlib.
