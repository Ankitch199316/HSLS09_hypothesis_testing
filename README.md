# 🧠 Investigating Socioeconomic Influence on Math Identity: HSLS:09 Data Analysis

## 📌 Project Overview

This project analyzes large-scale longitudinal education survey data to examine how **socioeconomic factors relate to student academic identity**, with a focus on math identity as an early indicator of educational outcomes.

Using the High School Longitudinal Study of 2009 (HSLS:09), the analysis applies statistical testing and regression techniques to identify meaningful differences across socioeconomic groups and to demonstrate how data-driven insights can inform targeted interventions and resource prioritization.


---

## 🗃️ Dataset Overview

The analysis uses data from the High School Longitudinal Study of 2009 (HSLS:09), a nationally representative survey administered by :contentReference[oaicite:0]{index=0}.

The dataset captures a broad range of student-level information, including socioeconomic indicators, academic outcomes, family background, and attitudinal measures. Given the scale and complexity of the data, careful variable selection and validation were required to ensure accurate interpretation.

Key variables were mapped using official documentation to translate coded fields into meaningful socioeconomic and academic indicators.

- **Source:** [NCES - HSLS:09 Public Use Dataset](https://nces.ed.gov/surveys/hsls09/)
- **Size:** ~600 MB across multiple files
- **Variables:** 9000+ columns covering academic performance, SES, identity, family background, future plans, and more

### ⚙️ Data Acquisition & Preparation
```python
# Downloaded from the NCES online portal (public use files)
# Initial file: ~600MB .txt and .sas files
# Read using pandas + manual variable selection

import pandas as pd

# Load subset for initial exploration
df = pd.read_csv("hsls09_data_subset.csv")
```

Before doing any analysis, I spent time reading the **extensive codebook** to map cryptic column names (e.g., `X1MTHID`, `X1SESQ5`) to their meanings. This was crucial for framing hypotheses meaningfully.

---

## 🎯 Analytical Questions

The analysis focuses on how different socioeconomic indicators relate to students’ math identity, an early signal linked to academic confidence and long-term educational outcomes.

Four analytical questions were examined to understand:
- Whether math identity differs meaningfully across socioeconomic groups
- How parental education and income relate to academic self-perception
- Whether multiple SES factors jointly explain variation in math identity

---

## 🔬 Hypothesis 1: SES Quintile vs. Math Identity
**H₀**: No difference in math identity across SES quintiles  
**H₁**: Higher SES quintiles have significantly higher math identity

### Statistical Method:
- One-Way ANOVA
- Tukey’s HSD Post-hoc Analysis

```python
from scipy.stats import f_oneway
import statsmodels.api as sm
```

**Key Result:** ANOVA F = 73.45, p < 0.0001 ✅

### 🔍 Interpretation:
- Students in the **highest SES quintile** had significantly stronger math identity than the lowest quintile.
- Differences were statistically significant across multiple SES levels.

<img width="1228" alt="Screenshot 2025-04-21 at 4 48 03 PM" src="https://github.com/user-attachments/assets/30ed5550-e044-4337-80a4-bb48802d3b91" />


---

## 🔬 Hypothesis 2: Parental Education vs. Math Identity
**H₀**: No difference in math identity across parental education levels  
**H₁**: Students with more educated parents have higher math identity

### Statistical Method:
- One-Way ANOVA
- Tukey’s HSD

```python
# Clean & group X1PAREDU + run ANOVA
```

**Key Result:** ANOVA F = 36.48, p < 0.0001 ✅

### 🔍 Interpretation:
- Students with parents holding **Ph.D./MD/Law degrees** had the highest average scores.
- Clear gaps between lower and higher education categories.

<img width="1220" alt="Screenshot 2025-04-21 at 4 47 20 PM" src="https://github.com/user-attachments/assets/fd39d651-2684-42ba-beca-7dbd7b87760a" />


---

## 🔬 Hypothesis 3: Family Income vs. Math Identity
**H₀**: No difference in math identity across income brackets  
**H₁**: Higher family income correlates with higher math identity

### Statistical Method:
- One-Way ANOVA
- Tukey’s HSD

```python
# Income bracket grouping via X1FAMINCOME
```

**Key Result:** ANOVA F = 9.88, p < 0.0001 ✅

### 🔍 Interpretation:
- Math identity improved with rising income.
- The **$235k+ group** showed significantly higher scores than lower-income peers.

<img width="1226" alt="Screenshot 2025-04-21 at 4 46 48 PM" src="https://github.com/user-attachments/assets/d11f8321-319b-4d68-b752-a2aaaba774fc" />


---

## 🔬 Hypothesis 4: Combined SES Factors vs. Math Identity
**H₀**: SES, parental education, and income do not jointly influence math identity  
**H₁**: These factors jointly predict math identity

### Statistical Method:
- Multiple Linear Regression (OLS)
- One-hot encoding of categorical vars

```python
X = df_encoded.drop("X1MTHID", axis=1)
y = df_encoded["X1MTHID"]
X = sm.add_constant(X)
model = sm.OLS(y, X).fit()
model.summary()
```

**Key Result:** R² = 0.027, p < 0.0001 ✅

### 🔍 Interpretation:
- SES score had strongest positive effect
- Some advanced degrees showed weak or negative coefficients
- Suggests possible multicollinearity or cultural factors

<img width="1066" alt="Screenshot 2025-04-21 at 4 46 23 PM" src="https://github.com/user-attachments/assets/5106fed0-b97d-420f-84b0-026ac6f96637" />


---

## 🧠 Summary of Findings
- SES is **positively correlated** with student math identity
- Parental education and income independently and jointly matter
- Social factors deeply influence students’ academic self-concept

## 🧩 Other Insights
- Many **SAT-related fields** in the dataset had invalid/missing values (e.g., `-5.0`)
- Variables like **number of parents in STEM** and **school support climate** could be explored further

---

## 📦 Project Files
- `HSLS09_Project.ipynb` — Python analysis notebook
- `h1_ses_vs_math_identity.csv` — Cleaned data for Dashboard 1
- `h2_parentedu_vs_math_identity.csv` — Dashboard 2
- `h3_income_vs_math_identity.csv` — Dashboard 3
- `regression_coefficients_plot.png` — Plot used in Dashboard 4
- Tableau dashboards (4 total)

---

## 🏁 Final Thoughts
This project not only highlights my ability to work with large survey datasets, but also showcases my proficiency in:
- **Data cleaning & feature engineering**
- **Statistical testing (ANOVA, regression)**
- **Tableau storytelling and dashboard design**
- **Clear insight communication** for non-technical stakeholders

**Thanks for reading!**


