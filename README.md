
---

# Dataset Information

- Dataset: **Default of Credit Card Clients (Taiwan, 2005)**  
- Total records: **30,000 clients**  
- Number of variables: **25**

| Feature | Description |
|----------|-------------|
| ID | Unique identifier for each client |
| LIMIT_BAL | Amount of given credit in NT dollars (includes individual and family/supplementary credit) |
| SEX | Gender (1 = male, 2 = female) |
| EDUCATION | (1 = graduate school, 2 = university, 3 = high school, 4 = others, 5–6 = unknown) |
| MARRIAGE | Marital status (1 = married, 2 = single, 3 = others) |
| AGE | Age in years |
| PAY_0 – PAY_6 | Repayment status for April–September 2005 (-1 = pay duly, 1–9 = delay in months) |
| BILL_AMT1 – BILL_AMT6 | Amount of bill statements (NT dollars) |
| PAY_AMT1 – PAY_AMT6 | Amount of previous payments (NT dollars) |
| default.payment.next.month | Default payment indicator (1 = yes, 0 = no) |

---

# Work Done

## 1. Exploratory Data Analysis & Understanding
- Loaded the dataset and inspected feature names, datatypes, and summary statistics.  
- Verified that there were **no explicit missing values**, but some undocumented codes were present in categorical columns.
- Identified inconsistent or undefined category values such as:
  - `MARRIAGE`: value `0` (undocumented)
  - `EDUCATION`: values `0`, `5`, and `6`
  - `PAY_0` to `PAY_6`: values `-2` and `0` (not matching the documentation)

## 2. Data Cleaning
- Created a clean copy of the dataset to preserve the original data.  
- Replaced undocumented or unknown category values:
  - `MARRIAGE`: 0 → 3 (Other)
  - `EDUCATION`: {0, 5, 6} → 4 (Other)
  - `PAY_*`: {0, -2} → -1 (Pay duly)
- Verified the unique values post-cleaning to ensure consistency.

**Observations:**
- These replacements aligned all categorical variables with the official documentation.
- The dataset retained its original shape (no rows were dropped).
- Data consistency improved for modeling and interpretation.

## 3. Handling Missing and Undocumented Values
- Treated the undefined category codes as equivalent to missing values.
- Encoded them appropriately during cleaning to maintain interpretability.
- This approach allowed modeling without discarding potentially informative samples.

## 4. Logistic Regression Model
- Implemented **Logistic Regression** to predict the likelihood of default payment.
- Target variable: `default.payment.next.month`
- Data split into training and test sets (80–20).
- Applied feature scaling to numerical variables for model stability.
- Evaluated performance using metrics such as **Accuracy**, **Precision**, **Recall**, and **F1-score**.

**Results:**
- Logistic Regression achieved reasonable predictive accuracy on the test set.
- Default class imbalance was observed (fewer defaults than non-defaults), which was considered during interpretation.
- Model coefficients showed strong relationships between repayment behavior (PAY_* variables) and the probability of default.

---

# Conclusion

- The dataset contained no explicit null values but had undocumented category codes that required cleaning.  
- After standardizing these values, Logistic Regression was successfully applied to model default probability.  
- The analysis confirmed that **repayment status, credit limit, and past payment behavior** were the strongest predictors of default.  
- Data cleaning played a critical role in ensuring valid and interpretable modeling outcomes.
