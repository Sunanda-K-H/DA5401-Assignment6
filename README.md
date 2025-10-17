# DA5401-Assignment6

**Name**: Kaki Hephzi Sunanda<br>
**Roll Number**: DA25M015<br>
**Date**: 04.09.2025<br>

---

# Repository Information
This repository contains the code for applying **Principal Component Analysis (PCA)** and **Logistic Regression** to the UCI Mushroom dataset.  
The assignment demonstrates how categorical features can be transformed, reduced in dimensionality, and evaluated for class separability.  

---

# Repository Structure

```
📦 assignment-2-Sunanda-K-H
├─ README.md
└─ DA5401_A2_DA25M015.ipynb
└─ plots/
```

---

# Dataset Information

- The dataset is the Mushroom dataset from the UCI Machine Learning Repository.
- It contains 8,124 rows and 23 attributes (including target `class`) describing physical characteristics of mushrooms.
- Each row represents a mushroom sample and includes attributes such as `cap-shape`, `cap-surface`, `cap-color`, `bruises`, `odor`, `gill-attachment`, `gill-size`, `gill-color`, `stalk-shape`, `stalk-root`, `stalk-surface`, `stalk-color`, `veil-type`, `veil-color`, `ring-number`, `ring-type`, `spore-print-color`, `population`, `habitat`.
- Target variable: `class`
  - e = edible
  - p = poisonous
- All features are categorical.
- veil-type contains only one category.
- `stalk-root` contains missing values represented by `?`.
- Dataset is balanced:
  - 51.8% edible (4208 samples).
  - 48.2% poisonous (3916 samples).

![Class Distribution](https://github.com/DA5401-JUL-NOV-2025/assignment-2-Sunanda-K-H/blob/main/plots/class_dist.png)

---

# Work Done
## 1. Exploratory Data Analysis & Preprocessing
- Dataset contained categorical features only.
- Applied One-Hot Encoding: expanded 22 features into 116 binary features.
- Standardized features to ensured equal contribution to PCA.

Observations:
- `veil-type` feature had only one category, thus it was dropped (has zero variance).
- `stalk-root` feature contained missing value marked as '?'. Instead of dropping, it was kept as a separate category since analysis showed it contributed variance.
- Analysis on `stalk-root` feature:
  - Heatmap of PCA loadings revealed that `?` had strong contributions to PC1 (0.5) & PC2 (0.7), as shown below.
  - This showed that missing value was not random but actually informative.

  ![Analysis - Missing Value](https://github.com/DA5401-JUL-NOV-2025/assignment-2-Sunanda-K-H/blob/main/plots/stalkroot.png)

## 2. PCA without restricting components
- Ran PCA on standardized features with all components.
- Generated Scree Plot and Cumulative Variance Plot.
- Key finding: 59 components retained 95% of variance, reducing dimensionality significantly (116 to 59).

## 3. Class Separability in PCA Space
- Scatter plots of the first 2–4 PCs showed edible and poisonous mushrooms forming distinct clusters.
- Some overlap remained, but overall separation was strong.

![PC](https://github.com/DA5401-JUL-NOV-2025/assignment-2-Sunanda-K-H/blob/main/plots/pc12.png)

- Below is the Pairwise Scatter plot for 2-4 PCs.
![PC14](https://github.com/DA5401-JUL-NOV-2025/assignment-2-Sunanda-K-H/blob/main/plots/pc14.png)


## 3. PCA with Variance Thresholds
- Tested thresholds: 85%, 90%, 95%, 99%.
- Results:
  - 42 PCs retained 85% variance.
  - 50 PCs retained 90% variance.
  - 59 PCs retained 95% variance.
  - 72 PCs retained 99% variance.
 
## 4. Classification with Logistic Regression
- Used Logistic Regression as a surrogate model to evaluate PCA-transformed data.
- Results:
  - With very few PCs, accuracy was low (~88%).
  - Accuracy increased with more PCs and stabilized at 100% beyond ~30 PCs.
  - At all variance thresholds (85–99%), perfect performance was observed.

![accuracy](https://github.com/DA5401-JUL-NOV-2025/assignment-2-Sunanda-K-H/blob/main/plots/acc.png)

---

# Conclusion

This assignment demonstrated how PCA can reduce dimensionality without sacrificing accuracy. Logistic Regression was used as a surrogate performance measure, confirming that PCA created a feature space where classes are linearly separable.
