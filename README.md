# VIPER — VUS Interpretation using Probabilistic Evidence and Random Forest

A machine learning framework for predictive interpretation of variants of uncertain significance (VUS) in hereditary cancer genomics.

## Key Results
- Best model: Random Forest (variant-level AUC-ROC = 0.961)
- VUS reclassified at >99% precision: 36.9% (21493 / 58249)
- Likely Pathogenic: 16211 | Likely Benign: 5,282 | Uncertain: 36756
- Thresholds: P > 0.80 (Likely Pathogenic) | P < 0.20 (Likely Benign)

## Notebooks — run in order
| Notebook | Description |
|---|---|
| `vus_eda_transcriptlevel.ipynb` | Data curation, VEP annotation processing, EDA, feature engineering |
| `vus_model_training.ipynb` | Model training and comparison (LR, SVM, RF, XGBoost) |
| `vus_shap_explainability.ipynb` | SHAP-based model explainability |
| `vus_patient_prediction.ipynb` | Patient variant prediction |

## Data
- ClinVar GRCh38 VCF (January 2026 release)
- FTP: https://ftp.ncbi.nih.gov/snp/latest_release/VCF/GCF_000001405.40.gz
- VEP v114.2 offline cache, GRCh38 assembly
- Training set: 35998 unique variants (28798 train / 7,200 test)

## Thresholds
Aligned with Tavtigian et al. (2020) Bayesian ACMG/AMP framework:
- Likely Pathogenic: P(Pathogenic) > 0.80 (validated precision = 0.990)
- Likely Benign: P(Pathogenic) < 0.20 (validated precision = 0.992)
- Uncertain: 0.20 <= P <= 0.80

## Requirements
See requirements.txt

## License
MIT
