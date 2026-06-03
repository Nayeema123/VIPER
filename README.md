# VIPER - VUS Interpretation using Probabilistic Evidence and Random Forest

A machine learning framework for predictive interpretation of variants of uncertain significance (VUS) in hereditary cancer genomics.
## Key Results

| Metric | Value |
|---|---|
| Test ROC-AUC (Random Forest) | 0.99+ |
| 10-fold CV AUC | 0.99 ± <0.01 |
| Overall concordance (ENIGMA) | 98.83% |
| Sensitivity | 99.98% |
| Specificity | 97.00% |
| VUS reclassified (of 40,894) | ~69.4% |
| High-confidence coverage | ~99% |

## What This Repository Contains
This repository covers the full VIPER analysis pipeline across five notebooks.
Notebook 1 — EDA and Data Preparation loads the ClinVar dataset, groups raw classification terms into Pathogenic, Benign, and VUS categories, performs exploratory data analysis across variant consequence, CADD PHRED score, population allele frequency, and VEP IMPACT categories, and produces the engineered feature matrix used for model training.
Notebook 2 — Model Training trains and compares four classifiers (Random Forest, XGBoost, SVM, Logistic Regression), tunes the top two using GridSearchCV with 5-fold cross-validation, evaluates performance with ROC and Precision-Recall curves including bootstrap confidence intervals, and defines the three-zone probabilistic classification scheme.
Notebook 3 — SHAP Analysis uses TreeExplainer to compute SHAP values on a stratified test sample, producing global feature importance rankings, a beeswarm plot showing directional feature effects, and dependence plots for the top three features (CADD PHRED, MAX_AF, PolyPhen Score).
Notebook 4 — VUS Reclassification applies the trained model to all 40,894 held-out VUS variants, reports reclassification outcomes across four probability thresholds, and characterises reclassified variants by gene, consequence type, hereditary cancer gene membership, and disease category.
Notebook 5 — ENIGMA BRCA Validation externally validates VIPER against ENIGMA BRCA Exchange classifications, annotates variants through the same VEP and CADD pipeline used in training, measures concordance, and evaluates agreement between VIPER's VUS reclassifications and ENIGMA's independent verdicts.

## Data Sources

ClinVar — variant classifications and condition metadata (GRCh38)
Ensembl VEP — functional annotations (consequence, IMPACT, SIFT, PolyPhen, gnomAD allele frequencies)
CADD v1.6 — pathogenicity scores via https://cadd.bihealth.org/score
BRCA Exchange — ENIGMA-classified BRCA1/BRCA2 variants for external validation

## Features Used
Nine variant-level features were used for classification: CADD PHRED score, maximum population allele frequency (MAX_AF), PolyPhen-2 score, VEP IMPACT category, variant class, transcript biotype, SIFT category, PolyPhen category, and grouped consequence type. SIFT score was excluded after correlation analysis due to collinearity with PolyPhen score.

## Classification Scheme

After training, variants are assigned to one of three zones based on predicted pathogenicity probability. Variants with probability ≥ 0.80 are reclassified as Pathogenic, those with probability <= 0.20 are reclassified as Benign, and those in between remain as VUS. The Pathogenic threshold was selected at the point on the Precision-Recall curve where precision ≥ 0.99 with maximum recall.

##  License
This project is for research use. Data sourced from ClinVar and BRCA Exchange is subject to their respective data use policies.
