# Online Fraud Detection MLOps Project

## Overview

This project trains and tunes Logistic Regression, Decision Tree, and Random Forest models for online fraud detection. The notebook uses SMOTE/SMOTENC inside GridSearchCV folds to prevent data leakage.

## Project structure

- `data/raw/`: original CSV dataset
- `notebooks/`: model development notebook
- `models/`: generated best model artifact
- `reports/metrics/`: generated comparison and tuning results
- `src/`: reusable inference code
- `api/`: FastAPI service
- `tests/`: automated tests
- `mlops/`: MLflow tracking script
- `azure/`: Azure ML endpoint assets
- `.github/workflows/`: GitHub Actions CI

## Local model development

1. Create and activate `.venv`.
2. Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

3. Put the CSV inside `data/raw/`.
4. Open `notebooks/01_fraud_detection_model_development.ipynb`.
5. Select the `Python - Fraud Detection` kernel.
6. Run the notebook sequentially.

The final artifact will be generated at:

```text
models/best_fraud_detection_smote_gridsearch.joblib
```

## Run FastAPI after model training

```powershell
python -m uvicorn api.main:app --reload
```

Open Swagger at `http://127.0.0.1:8000/docs`.

## Run tests

```powershell
python -m pytest -v
```

## Track the model with MLflow

```powershell
python mlops/track_model.py
mlflow ui
```

## Azure deployment

After registering the model as `fraud-detection-model`, deploy using the YAML assets inside `azure/`.
