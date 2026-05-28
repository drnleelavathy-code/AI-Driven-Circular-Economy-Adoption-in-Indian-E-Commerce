# Consumer Drivers of Circular Economy Adoption in Indian E-Commerce
### A Hybrid RF–ARIMAX Modelling and Scenario Forecasting Approach

[![Python 3.12](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Journal: TFSC](https://img.shields.io/badge/Journal-Technological%20Forecasting%20%26%20Social%20Change-orange)](https://www.journals.elsevier.com/technological-forecasting-and-social-change)

---

## Overview

This repository contains the full reproducible codebase for:

> **Kalidindi R., Narkedamilly L., Uma Meghana S. (2025)**
> *Consumer Drivers of Circular Economy Adoption in Indian E-Commerce: A Hybrid RF–ARIMAX Modelling and Scenario Forecasting Approach*
> 

The study models circular economy (CE) adoption behaviour among Indian e-commerce consumers using a **Random Forest (RF)** regressor as the primary model, benchmarked against Linear Regression, ElasticNet, HistGradientBoosting, XGBoost, and LightGBM. Time-series forecasting is performed using **ARIMAX** on quarterly GMV data. SHAP values, Boruta feature selection, Granger causality, and subgroup analyses are included.

---

## Key Results

| Model | R² | MAE | RMSE |
|---|---|---|---|
| **Random Forest** | **0.9721** | **0.0287** | **0.0358** |
| HistGradientBoosting | 0.9693 | 0.0288 | 0.0376 |
| XGBoost† | ≈0.970 | — | — |
| LightGBM† | ≈0.969 | — | — |
| Linear Regression | 0.5199 | 0.1189 | 0.1485 |
| ElasticNet | ~0.52 | — | — |

> † XGBoost and LightGBM results are from a supplementary run with optional packages installed (`xgboost==3.2.0`, `lightgbm==4.6.0`).

**RF vs LR improvement: +87.0% R²** (>40% confirmed ✓)
**Top-3 MDI features: 98.9% | SHAP top-3 combined: ≈83.0%**

---

## Repository Structure

```
rf-arimax-sustainability-india/
│
├── ritesh_merged_code_4.py        # Main analysis script (v12 final)
├── requirements-full.txt          # All dependencies combined
├── .gitignore                     # Git ignore rules
├── LICENSE                        # MIT License
├── README.md                      # This file
│
└── results/                       # Auto-generated on first run
    ├── figures/                   # Figs 1–5 (TIFF, 300 DPI)
    ├── tables/                    # Model comparison, segmentation, GMV CSVs
    └── supplementary/             # Tables A1–A9, supplementary figures
```

---

## Quickstart

### 1. Clone the repository
```bash
git clone https://github.com/drnleelavathy-code/rf-arimax-sustainability-india.git
cd rf-arimax-sustainability-india
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

To reproduce XGBoost, LightGBM, SHAP, and Boruta sections:
```bash
pip install -r requirements-optional.txt
```

### 3. Run the analysis
```bash
python ritesh_merged_code_4.py
```

All outputs are saved to `results/figures/`, `results/tables/`, and `results/supplementary/`.

---

## Features & Methodology

### Dataset
- **N = 50,000** synthetic Indian e-commerce consumers
- **12 theory-mapped features** calibrated to published Indian survey sources (MoSPI, IBEF, CSE, Deloitte India)
- Pure-nonlinear Data Generating Process (DGP): `LIN_VAR = 0.00`

### Features
| Feature | Description | Calibration Source |
|---|---|---|
| `x_aware` | CE awareness | Deloitte India 2023 |
| `x_avail` | Product availability | CSE 2023 |
| `x_price` | Price sensitivity | CSE 2023 |
| `x_age` | Consumer age group | Uniform proxy |
| `x_tier` | City tier (1/2/3) | IBEF 2024 |
| `x_income` | Income (Beta-calibrated) | MoSPI HCE 2022-23 |
| `x_quality` | Quality perception | CSE 2023 |
| `x_env_concern` | Environmental concern | Paul et al. 2016 |
| `x_social_norm` | Social norms | Yadav & Pathak 2016 |
| `x_trust` | Platform trust | Jaiswal & Kant 2018 |
| `x_prior_ce` | Prior CE experience | Deloitte India 2023 |
| `x_device` | Device type | MeitY 2023 |

### Analysis Sections (17 Steps)
1. Synthetic dataset generation
2. Fidelity tests (KS + Wasserstein)
3. SMOTE diagnostics
4. Model training (RF, HistGB, LR, ElasticNet, XGBoost, LightGBM)
5. SHAP TreeExplainer
6. Boruta feature selection
7. Permutation importance
8. ARIMAX forecasting (quarterly GMV, n=40)
9. Granger causality tests
10. Segmentation analysis (age, tier, income)
11. Within-tier RF subgroup analysis
12. Nonlinear residual analysis (Figs 1–5)
13. Comprehensive tables
14. Run metadata export

---

## Reproducibility

```
Python   : 3.12
Seed     : 42
N        : 50,000
n_trees  : 200
max_depth: 20
max_feat : 8
n_jobs   : -1
```

All random states are fixed via `seed=42`. Results are fully deterministic.

---

## Outputs

### Figures (results/figures/)
- `Fig1_` — Feature importance (MDI)
- `Fig2_` — Partial dependence plots
- `Fig3_` — Segmentation analysis
- `Fig4_` — ARIMAX forecast
- `Fig5_nonlinear_residuals.tif` — LR residuals vs nonlinear interaction terms

### Tables (results/tables/)
- `Table2a_sweep_summary.csv` — Hyperparameter sweep
- `Table3_model_comparison.csv` — All model metrics
- `run_metadata_v12.json` — Full run metadata
- `synthetic_consumer_dataset.csv` — Generated dataset

### Supplementary (results/supplementary/)
- `Table_A1_fidelity.csv` — Wasserstein fidelity tests
- `Table_A1b_SMOTE_distribution.csv` — SMOTE diagnostics
- `Table_A2_boruta.csv` — Boruta feature selection
- `Table_A3_permutation_importance.csv` — Permutation + SHAP importance
- `Table_A5_within_tier.csv` — Within-tier RF subgroup analysis
- `Table_A8_complexity_bigO.csv` — Algorithm complexity

---



---

## License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---
