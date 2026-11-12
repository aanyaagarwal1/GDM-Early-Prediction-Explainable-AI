# Methodology

## Dataset and predictors
The paper describes a public dataset of 3,525 records, 15 clinical attributes, and a binary GDM outcome. Predictors include demographic, physiological, medical-history, and lifestyle variables. The case-number identifier is excluded from model inputs. OGTT is excluded from the primary prediction feature set.

## Preprocessing and feature engineering
The reported workflow removes duplicate rows, imputes missing numerical values with medians and binary values with modes, and clips numerical outliers using IQR limits. It engineers BMI category, age group, blood-pressure category, and a heuristic composite Risk Score. The paper explicitly describes the Risk Score as a heuristic, not a validated clinical scoring system.

## Model development
Six classifiers are compared: Logistic Regression, Random Forest, Extra Trees, XGBoost, LightGBM, and CatBoost. Randomized hyperparameter search uses stratified five-fold cross-validation with ROC-AUC as the selection metric. The dataset is split 80:20 using stratification; SMOTE is applied only to the training partition.

## OGTT ablation
Two otherwise comparable experiments are run: with OGTT and without OGTT. The OGTT-excluded experiment is used for final model selection, SHAP interpretation, and the clinical prediction module.

## Explainability
SHAP is used for global feature influence and patient-level waterfall explanations. These are explanations of fitted model behavior, not causal effects.

## LLM-assisted report analysis
Gemini 3.1 Flash-Lite extracts Age, BMI, HDL, Hemoglobin, Systolic BP, Diastolic BP, and Gestation Weeks from PDF/image inputs. Missing fields are requested as null. The LLM is an extraction/structuring layer; the supervised ML model generates the GDM prediction.
