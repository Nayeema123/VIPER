# VIPER - VUS Interpretation using Probabilistic Evidence and Random Forest

## Overview
A machine learning framework for computational reclassification of 
variants of uncertain significance (VUS) in hereditary cancer genomics.
Trained on 104,646 high-confidence ClinVar germline variants (3★+) 
with external validation on 7,462 ENIGMA-classified BRCA1/BRCA2 variants.

## Performance
- Test ROC-AUC: 0.9995 (95% CI: 0.9993-0.9997)
- 10-fold CV AUC: 0.9992 ± 0.0004
- ENIGMA concordance: 98.83%
- VUS concordance: 89.57%

## Pipeline
1. Data preparation (ClinVar + VEP + CADD)
2. Exploratory data analysis
3. Feature engineering
4. Model training (RF, XGBoost, SVM, LR)
5. Test evaluation + threshold derivation
6. SHAP explainability
7. VUS reclassification
8. External validation (ENIGMA BRCA Exchange)

## Requirements
See requirements.txt
