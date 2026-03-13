# Assisted Living Market Analysis
### Predicting Facility Saturation Across Minnesota Counties

> **Tools:** Python · Scikit-learn · Random Forest · Pandas · Matplotlib  
> **Type:** Case Study

---

## Background

Population predictions for the next 20 years -> 
```
Ages 65 and older will nearly double
Ages 85 and older will increase by over 100%
```
This demographic shift will significantly increase the need for assisted living facilities.

Understanding how socioeconomic factors influence our current supply of assisted living facilities is key to addressing future demand and ensuring equitable access to care.

---

## Research Question

Can socioeconomic factors be used to classify Minnesota counties into Low, Medium, or High saturation of assisted living facilities per 1,000 elderly residents using a Random Forest Classifier?

**Hypothesis:** Socioeconomic factors predict facility saturation in Minnesota counties better than random chance.

---

**Assisted Living Facility Saturation:** The number of assisted living facilities in a county per 1,000 elderly residents (65+).

**Socioeconomic Factors considered:**
- Elderly Population (65+)
- Total Population
- Poverty Rate
- Unemployment Rate
- Median Household Income
- Median Home Value of Owned Homes
- Less Than High School Diploma Rate
- College Education or Higher Rate
- Median Age
---

## Data

- **Population data** — Minnesota 2020 Decennial Demographic Profile, U.S. Census Bureau
- **Facility data** — Assisted living facility dataset from a peer-reviewed research publication (Stengel et al., 2022), filtered to Minnesota counties

**Scope:** Counties with total population > 20,000

---

## Process

- Cleaning and restructuring the population + facility datasets for consistency
- Merging on shared counties
- Creation of target variable: Facility Saturation per 1,000 Elderly Residents
- Categorized counties by `Low`, `Medium`, and `High` saturation
- Trained with Random Forest Classifier, optimized with `RandomizedSearchCV`

---

## Results

After hyperparameter optimization, the Random Forest model achieved **90% predictive accuracy**, a 10% improvement from default settings.

| Model | Accuracy | Weighted F1 |
|---|---|---|
| Baseline Random Forest | 80% | 0.71 |
| Tuned Random Forest | **90%** | **0.85** |

**Best parameters:** `n_estimators=200`, `max_depth=20`, `min_samples_leaf=2`, `min_samples_split=5`

This result validates the hypothesis, facility saturation per 1,000 elderly residents is predicted by socioeconomic factors better than random chance.

---

## Key Findings

**Most influential predictors:**

| Rank | Feature | Importance |
|---|---|---|
| 1 | Total Population | 0.179 |
| 2 | Median Home Value of Owned Homes | 0.164 |
| 3 | Less Than High School Diploma Rate | 0.138 |
| 4 | Elderly Population (65+) | 0.133 |
| 5 | Poverty Rate | 0.129 |

- Counties with **low home values and smaller elderly populations** were most likely to fall into Low Saturation
- Counties with **high home values but smaller total populations** were most likely to fall into High Saturation

---

## Limitations

- Excluding counties with total populations below 20,000 introduces sampling bias, skewing data toward higher-population counties
- Random Forest feature importances do not quantitatively measure the effect of each predictor: results are relative, not conclusive
- Predictor contributions may be exaggerated as not all possible socioeconomic factors are considered.

---

## Proposed Next Steps

- Validate results with logistic regression to provide statistically testable findings
- Expand with feature engineering, for example: deriving an Elderly Poverty Rate to capture additional interactions
- Replicate nationwide using U.S. Census Bureau data and the same facility dataset to guide broader range investment decisions

---

## Files

```
assisted-living-market-analysis/
├── README.md
├── notebooks/
│   └── balanced_random_forest_assisted_living.ipynb
├── data/
│   ├── assisted-living-facilities.csv
│   └── DECENNIALDP2020.DP1.csv
└── visuals/
    ├── random_forest_feature_importance.png
    ├── facility_saturation_by_county.png
    └── decision_tree_random_forest.png
```

---

**Author:** Ameera Hassan · [LinkedIn](https://linkedin.com/in/ameerafhassan) · [Portfolio](https://ameerahassan.my.canva.site/)

---

## References

- Rubin, E., Schmidt, E., & Vorrasi, E. (2024, January 25). *Assisted living statistics.* ConsumerAffairs. https://www.consumeraffairs.com/assisted-living/statistics.html

- Stengel, A., Altosaar, J., Dittrich, R., & Elhadad, N. (2022). *Assisted living in the United States: An open dataset* [Preprint]. arXiv. https://doi.org/10.48550/arXiv.2212.14092

- Stengel, A., Altosaar, J., Dittrich, R., & Elhadad, N. (2022). *assisted-living-data* [Data and code repository]. GitHub. https://github.com/antonstengel/assisted-living-data

- U.S. Census Bureau. (2020). *DP1: Profile of general population and housing characteristics; Decennial Census 2020* [Table]. https://data.census.gov/table/DECENNIALDP2020.DP1?g=040XX00US27%2C27%240500000

- scikit-learn developers. (n.d.). *RandomForestClassifier.* https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html

- GeeksforGeeks. (2025). *Random forest hyperparameter tuning in Python.* https://www.geeksforgeeks.org/machine-learning/random-forest-hyperparameter-tuning-in-python/

- Sruthi. (2025). *Random Forest algorithm in machine learning.* Analytics Vidhya. https://www.analyticsvidhya.com/blog/2021/06/understanding-random-forest/
