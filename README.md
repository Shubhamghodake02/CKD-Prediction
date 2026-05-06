# CKD Prediction — EHR Analytics Pipeline

Binary classification pipeline to predict Chronic Kidney Disease (CKD) using anonymized Electronic Health Record (EHR) data.

---

## Project Structure

```
ckd-prediction/
├── ckd_raw_data.csv                  # Raw dataset (synthetic, anonymized)
├── week1_data_preprocessing.py       # Data cleaning & imputation
├── week2_eda_analysis.py             # EDA, biomarker correlations, visualisations
├── week3_modeling.py                 # ML models, SMOTE, hyperparameter tuning
├── week4_evaluation_dashboard.py     # Clinical evaluation & dashboard export
├── .gitignore
└── README.md
```

## Approach

| Week | Focus | Key outputs |
|------|-------|-------------|
| 1 | Data cleaning & imputation | `ckd_cleaned.csv`, missing data chart |
| 2 | EDA & correlation analysis | Heatmap, violin plots, pairplot |
| 3 | Modeling & tuning | LR + RF models, ROC curves, feature importance |
| 4 | Clinical evaluation & reporting | Confusion matrices, dashboard, risk profiles |

---

## Why Recall is the Priority Metric

In CKD screening, a **False Negative** (model predicts healthy, patient actually has CKD) is far more costly than a **False Positive** (unnecessary follow-up test). Early-stage CKD is asymptomatic — by the time clinical symptoms appear, irreversible kidney damage has often already occurred.

We therefore optimise for **Recall (sensitivity)** and accept lower Precision as the clinical tradeoff.

---

## Ethical Considerations

- All data is synthetic / de-identified. No real patient records are used or stored.
- No PHI or HIPAA-regulated identifiers are present anywhere in this repository.
- Models are evaluated for bias across age groups using stratified metrics.
- Raw data files are excluded from git via `.gitignore`.
- All API keys and credentials must be injected via environment variables — never hardcoded.

---
## Tech Stack

- **Python 3.10+**
- pandas, scikit-learn, imbalanced-learn (SMOTE)
- matplotlib, seaborn
- joblib (model persistence)
- Tableau / Power BI — for `patient_risk_profiles.csv` dashboard

---
