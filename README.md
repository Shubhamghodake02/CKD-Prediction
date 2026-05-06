# CKD Prediction — End-to-End EHR Analytics Pipeline

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

**Generated outputs (not committed — see .gitignore):**
```
ckd_cleaned.csv
model_logistic_regression.pkl
model_random_forest.pkl
scaler.pkl
feature_importance.csv
model_metrics.csv
patient_risk_profiles.csv
week1_*.png  week2_*.png  week3_*.png  week4_*.png
```

---

## Quickstart

### Google Colab
```python
# Upload ckd_raw_data.csv first, then run each script in order:
# 1. week1_data_preprocessing.py
# 2. week2_eda_analysis.py
# 3. week3_modeling.py
# 4. week4_evaluation_dashboard.py
```

### Local / Jupyter
```bash
pip install pandas scikit-learn imbalanced-learn matplotlib seaborn joblib
jupyter notebook
```
Run the four scripts in order — each saves its outputs for the next script to pick up.

---

## Dataset

**Source:** Synthetic dataset generated to mirror the [UCI CKD Dataset](https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease).
- 400 patient records, 24 clinical features, 1 binary target
- ~8% missing values in numeric columns (realistic EHR noise)
- Features include: serum creatinine, hemoglobin, blood urea, blood pressure, blood glucose, albumin, sodium, and more

**No real patient data is used.** All records are synthetically generated. No Protected Health Information (PHI) is present.

---

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

## Environment Variables

If connecting to cloud storage or databases, use environment variables:
```python
import os
db_host = os.environ.get('DB_HOST')
api_key = os.environ.get('API_KEY')
```
Never commit credentials to git.

---

## Tech Stack

- **Python 3.10+**
- pandas, scikit-learn, imbalanced-learn (SMOTE)
- matplotlib, seaborn
- joblib (model persistence)
- Tableau / Power BI — for `patient_risk_profiles.csv` dashboard

---

## Commit Convention

```
data-clean: imputed missing numeric values with column medians
eda: added correlation heatmap and violin plots for key biomarkers
model: trained Random Forest with GridSearchCV, recall=0.94
docs: added clinical evaluation section and README
```
Minimum 3–5 meaningful commits per active development day.
