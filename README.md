# Hospital Capacity Stress Prediction

## Project Overview

This project simulates hospital admissions and models the probability of hospital capacity stress using logistic regression.

Capacity stress is defined as a situation where bed occupancy exceeds available beds.

The goal is to demonstrate:
- Synthetic healthcare data generation
- Dynamic occupancy modeling
- Logistic regression classification
- Model evaluation under class imbalance
- Interpretation of coefficients using odds ratios

---

## Data Generation

A synthetic dataset of 200 days was generated.

Variables:
- `admissions`: daily hospital admissions (Poisson distributed)
- `avg_length_of_stay`: average length of stay (3–6 days)
- `available_beds`: fixed at 160
- `occupancy`: dynamically computed based on past admissions and LOS
- `capacity_stress`: binary target variable

Occupancy is calculated as:

Occupancy_t = sum of all past admissions still within their LOS window.

---

## Modeling Approach

Logistic regression was used to predict capacity stress from:

- admissions
- average length of stay

Occupancy was intentionally excluded from the feature set to prevent data leakage.

Data was split:
- 70% training
- 30% testing

---

## Results

Test set performance:

- Accuracy: 0.90
- ROC AUC: ~0.49

However, the model predicted only the majority class (stress).

Class imbalance:
- Stress days ≈ 90%
- Non-stress days ≈ 10%

This resulted in:
- Perfect recall for stress
- Zero recall for non-stress

This highlights the importance of evaluating models beyond accuracy in imbalanced datasets.

---

## Coefficient Interpretation

| Feature | Coefficient | Odds Ratio |
|----------|------------|------------|
| admissions | 0.039 | 1.04 |
| avg_length_of_stay | -0.102 | 0.90 |

Interpretation:

- Each additional admission increases the odds of stress by ~4%.
- Longer length of stay slightly decreases odds in this synthetic setup.
- Results are influenced by the synthetic data structure.

---

## Key Learnings

- Avoid data leakage (occupancy excluded)
- Accuracy can be misleading under class imbalance
- Precision and recall provide deeper insight
- Logistic regression offers interpretability
- Synthetic simulations can reveal structural modeling issues

---

## Future Improvements

- Address class imbalance (class weighting or resampling)
- Add seasonal admission effects
- Use real hospital datasets
- Explore threshold tuning

---

## Conclusion

This project demonstrates an end-to-end ML workflow in a healthcare-inspired scenario:

Data simulation → Feature engineering → Modeling → Evaluation → Interpretation.

It emphasizes the importance of model diagnostics and responsible evaluation in imbalanced settings.
