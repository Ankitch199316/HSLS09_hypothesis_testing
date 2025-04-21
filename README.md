# 🧠 Investigating Socioeconomic Influence on Math Identity: HSLS:09 Data Analysis

## 📌 Project Motivation
As part of my data analytics portfolio, this project was designed to demonstrate my ability to work with real-world educational survey data, perform statistical analysis, generate insights, and communicate findings through both code and visualization tools. 

In this case, I analyzed the **High School Longitudinal Study of 2009 (HSLS:09)** to explore the impact of **socioeconomic status (SES)** on students’ **math identity** — a key psychological metric linked to academic and career trajectories.

The aim was to:
- Showcase **statistical rigor** (ANOVA, regression, post-hoc analysis)
- Work with **messy real-world data** and detailed codebooks
- Demonstrate ability to tell a **clear story using Tableau** dashboards
- Deliver practical, **actionable insights for education policy**

---

## 🗃️ Dataset Overview
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

## 🎯 Hypotheses & Analysis
To frame the investigation, I focused on **four hypotheses** exploring how different SES indicators relate to students’ **Math Identity Score** (`X1MTHID`).

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

<img width="1226" alt="Screenshot 2025-04-21 at 4 35 33 PM" src="https://github.com/user-attachments/assets/b3197443-f9fc-4462-843d-468dada83537" />

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

<img width="1217" alt="Screenshot 2025-04-21 at 4 36 02 PM" src="https://github.com/user-attachments/assets/0029f225-7404-4fad-b45c-389d6fbc5042" />


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

<img width="1220" alt="Screenshot 2025-04-21 at 4 36 34 PM" src="https://github.com/user-attachments/assets/04db3309-4c15-44bc-839d-d3a364698b50" />


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

<img width="1175" alt="Screenshot 2025-04-21 at 4 37 05 PM" src="https://github.com/user-attachments/assets/2a4ab60f-af58-4b29-a1f6-0e9f81e7c028" />


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

