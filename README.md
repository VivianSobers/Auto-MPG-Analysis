# Auto-MPG-Analysis

## Overview

This project analyses `auto_mpg_data.csv` — a dataset of **398 automobile records** with specifications like fuel efficiency, engine size, weight, and origin. The analysis spans three units covering descriptive statistics, point estimation, and hypothesis testing with regression.

---

## Dataset

**File:** `auto_mpg_data.csv`  
**Shape (raw):** 398 rows × 9 columns  
**Shape (after cleaning):** 357 rows × 9 columns  
**Features used:** `mpg`, `cylinders`, `displacement`, `horsepower`, `weight`, `acceleration`, `model year`, `origin`  
**Excluded:** `car name`

---

## What It Does

### Unit 1 — Descriptive Statistics and Sampling Distributions

#### 1. Data Preprocessing
- Replaced `'?'` placeholders with `NaN`
- Imputed missing `horsepower` values with **median (95.0)**
- Dropped rows with missing `mpg` or `weight`
- Removed duplicate records — **0 duplicates** found
- Final shape: **(357, 9)**

#### 2. Descriptive Statistics

| Variable | Mean | Median | Std | Min | Max |
|----------|------|--------|-----|-----|-----|
| mpg | 24.04 | 23.00 | 8.47 | 9.0 | 82.53 |
| weight | 3008.94 | 2815.00 | 1040.43 | 1613.0 | 12174.14 |
| horsepower | 103.60 | 95.00 | 37.07 | 46.0 | 230.0 |
| acceleration | 15.60 | 15.50 | 2.73 | 8.0 | 24.8 |
| displacement | 192.71 | 146.00 | 103.05 | 68.0 | 455.0 |

**Skewness:** mpg=1.22 · weight=2.98 · horsepower=1.18 · acceleration=0.35 · displacement=0.70  
**Kurtosis:** mpg=5.27 · weight=20.75 · horsepower=1.09 · acceleration=0.58 · displacement=-0.76

#### 3. Key Inferences
- Strong negative relationship between `mpg` and `weight`, `displacement`, `horsepower`
- Most variables are right-skewed — distributions deviate from normality
- `weight` has extreme kurtosis (20.75), indicating heavy tails with outliers

#### 4. Outlier Detection (IQR Method)

| Variable | Outliers (out of 357) |
|----------|-----------------------|
| weight | 3 |
| horsepower | 21 |
| acceleration | 11 |

After removing outliers: shape changed from **(357, 9) → (325, 9)**

#### 5. Normality Testing
- **D'Agostino's K² test** for MPG: statistic=107.33, p-value≈0.000
- **Shapiro-Wilk test** for MPG: statistic=0.9287, p-value≈0.000
- Both tests reject normality (p < 0.05); Q-Q plot shows deviation from the 45° reference line

#### 6. Correlation with MPG

| Variable | Correlation with MPG |
|----------|---------------------|
| acceleration | +0.353 (positive) |
| weight | −0.488 |
| horsepower | −0.665 |
| displacement | **−0.737** (strongest negative) |

---

### Unit 2 — Point Estimation, MLE, Confidence Intervals

#### 7. Confidence Interval for Mean MPG (95%)
- Sample mean = 24.04, std = 8.47, n = 357
- **95% CI: (22.98, 24.66)**

#### 8. Margin of Error for Mean Horsepower

| Confidence Level | Margin of Error |
|-----------------|-----------------|
| 90% | 3.2356 |
| 95% | 3.8585 |
| 99% | 5.0809 |

Higher confidence → wider interval → less precision (precision–confidence trade-off).

---

### Unit 3 — Hypothesis Testing and Simple Linear Regression

#### 9. U.S. vs Japan MPG (Welch's t-test)
- USA: n=215, mean MPG = 20.57
- Japan: n=59, mean MPG = 31.13
- t-statistic = −12.64, **p-value ≈ 0.000**
- **Result:** Reject H₀ — Japanese cars have significantly higher mean fuel efficiency than US cars (α=0.05)

#### 10. Weight–MPG Correlation
- Pearson r = −0.4884, p-value ≈ 0.000
- Moderate negative association — heavier cars tend to have lower fuel efficiency

#### 11. Linear Regression: MPG ~ Weight
- **Equation:** `MPG = 35.9986 + (−0.003975) × Weight`
- **R² = 0.2385** — weight alone explains ~24% of variance in MPG
- Limitations: ignores other predictors (displacement, horsepower), potential non-linearities

---

## How to Run

### 1. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy statsmodels openpyxl
```

### 2. Open the notebook

```bash
jupyter notebook AutoMPG.ipynb
```

### 3. Place files in the same directory

```
auto-mpg-analysis/
├── AutoMPG.ipynb
├── auto_mpg_data.xlsx
├── Analysis_Report.pdf
└── README.md
```

---

## Key Findings

- Heavier, high-displacement, high-horsepower cars consistently have **lower fuel efficiency**
- Japanese cars average **~10.5 MPG more** than US cars — a statistically significant difference
- MPG distribution is **non-normal** (right-skewed, leptokurtic) — confirmed by both Shapiro-Wilk and D'Agostino tests
- Simple linear regression on weight alone achieves R²=0.24; a multi-feature model would perform significantly better

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| `Pandas` | Data cleaning, imputation, descriptive stats |
| `NumPy` | Numerical computation |
| `Matplotlib` / `Seaborn` | Visualizations |
| `Scipy` | t-tests, normality tests, correlation |
| `Statsmodels` | Q-Q plots |
| `Scikit-learn` | Linear regression |

---

## Author

**Vivian Sobers E** — [github.com/VivianSobers](https://github.com/VivianSobers)