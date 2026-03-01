# Antibiotic Resistance Prediction for UTI Treatment

Machine learning model predicting Ciprofloxacin resistance in urinary tract infections using clinical data from Stanford Healthcare.

## Project Overview

**Problem**: Physicians prescribe antibiotics empirically before lab results (48-72 hours), leading to 18% treatment failures when resistance is present.

**Solution**: Predictive model using patient demographics, hospital context, and medication history to guide antibiotic selection at point of care.

**Impact**: 79.3% AUC achieving 70% detection of resistant cases → $127M potential annual savings in US healthcare.

---

## Key Results

| Metric | Value |
|--------|-------|
| **AUC** | 79.3% |
| **Accuracy** | 71% |
| **Recall (Resistant)** | 70% |
| **Dataset Size** | 10,494 UTI cases |
| **Top Predictor** | Prior Ciprofloxacin use (19.8%) |

---

## Dataset

**Source**: [Stanford ARMD Dataset](https://datadryad.org/stash/dataset/doi:10.5061/dryad.jq2bvq8kp)
- 283,715 unique patients
- 15+ years (1999-2024)
- 55 antibiotics tested
- De-identified EHR data

**Filtered Scope**: Urine cultures with Ciprofloxacin susceptibility testing

---

## Tech Stack

- **Platform**: KNIME Analytics Platform
- **Algorithm**: Gradient Boosted Trees
- **Techniques**: SMOTE (class balancing), Feature Engineering, Hyperparameter Tuning
- **Evaluation**: ROC/AUC, Confusion Matrix, Feature Importance

---

## Project Structure
```
├── workflows/
│   └── ARMD_prediction.knwf          # Complete KNIME workflow
├── data/
│   └── README.md                      # Data download instructions
├── results/
│   ├── roc_curve.png                  # Model performance
│   ├── confusion_matrix.png           # Classification results
│   └── feature_importance.csv         # Predictor rankings
├── docs/
│   ├── technical_report.pdf           # Full methodology
│   └── presentation.pdf               # Executive summary
└── README.md
```

---

## Quick Start

### Prerequisites
```bash
- KNIME Analytics Platform 5.x
- 8GB+ RAM
- Dataset downloaded from Dryad
```

### Run Workflow
1. Download Stanford ARMD dataset
2. Open `ARMD_prediction.knwf` in KNIME
3. Configure CSV Reader paths to your data location
4. Execute workflow (⏱️ ~10 minutes)

---

##  Methodology

### Data Pipeline
```
283,715 patients → Filter: URINE (176k) → Filter: Positive (136k) 
→ Filter: Ciprofloxacin (10.5k) → SMOTE Balance → Train/Test Split (70/30)
```

### Feature Engineering
- **Age Risk Categories**: Low (<35), Medium (35-64), High (65+)
- **Ward Risk Score**: ICU (3) > ER (2) > Inpatient (1) > Outpatient (0)
- **Recent Antibiotic Exposure**: Binary flag for use within 30 days

### Model Optimization
- Class balancing: SMOTE (82/18 → 50/50)
- Algorithm: Gradient Boosted Trees
- Hyperparameters: Learning rate 0.1, 200 trees, depth 6

---

##  Key Findings

### Top 5 Predictors
1. **E. coli organism** (24.5%) - Most common, generally susceptible
2. **Prior Ciprofloxacin use** (19.8%) - Strongest modifiable risk factor
3. **Patient age** (13.2%) - Elderly have higher resistance
4. **Ward risk score** (8.9%) - ICU patients highest risk
5. **Pseudomonas organism** (7.6%) - Intrinsically resistant

### Clinical Impact
- **70% of resistant cases detected** before wrong prescription
- **9% false alarm rate** (acceptable trade-off in medicine)
- **Validates stewardship policies**: Avoid repeat Ciprofloxacin use

---

##  Business Value

### Cost-Benefit Analysis
- **Current annual failures**: 1.8M (US) × $350/failure = $630M wasted
- **With model**: Prevent 70% = $441M saved
- **Implementation cost**: $180M (one-time)
- **ROI**: 2.4x in year 1, infinite thereafter

---

## Visualizations

### ROC Curve
![ROC Curve](results/roc_curve.png)

### Confusion Matrix
![Confusion Matrix](results/confusion_matrix.png)

### Feature Importance
![Feature Importance](results/feature_importance.png)

---

##  Limitations

- **Geographic**: Stanford Healthcare (California) only
- **Temporal**: Training data through January 2024
- **Scope**: Ciprofloxacin and UTIs only (not other antibiotics/infections)
- **Validation needed**: External hospital systems before deployment

---

##  Future Work

- [ ] Add lab values (WBC, creatinine) with smart imputation
- [ ] Expand to other antibiotics (all 55 in dataset)
- [ ] Include blood and respiratory cultures
- [ ] External validation (different hospital systems)
- [ ] Real-time EHR integration prototype

---

##  References

- Nateghi Haredasht, F., et al. (2025). *Antibiotic Resistance Microbiology Dataset (ARMD)*. Dryad Digital Repository.
- Yahav, D., et al. (2020). Predicting resistance in gram-negative bacteria. *Clinical Infectious Diseases*.
- Murray, C.J., et al. (2022). Global burden of antimicrobial resistance. *The Lancet*.

---

##  Citation

If you use this work, please cite:
```bibtex
@misc{armd_prediction_2025,
  title={Machine Learning for Antibiotic Resistance Prediction in UTIs},
  author={[Your Name]},
  year={2025},
  institution={[Your University]},
  note={Academic project using Stanford ARMD dataset}
}
```


##  License

This project is for academic/educational purposes. Dataset usage subject to Stanford Healthcare and Dryad terms.

---

##  Acknowledgments

- Stanford Healthcare for publishing the ARMD dataset
- KNIME Analytics Platform for visual workflow tools
- Claude AI for project guidance and troubleshooting

---

**⭐ Star this repo if you found it useful!**
