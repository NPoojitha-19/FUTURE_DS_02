# Customer Retention & Churn Analysis

Customer churn analysis built for a Data Science & Analytics internship task. The project cleans telecom subscription data, analyzes churn patterns across contract types, tenure groups, internet services, and payment methods, and presents findings in an interactive Power BI dashboard and written insights report.

## Objective

Analyze customer behavior data the way a real retention analyst would, answering:
- Why are customers leaving the platform?
- Which customer segments are most likely to churn?
- How long do customers typically stay active?
- What actions can improve customer retention?

## Dataset

**Telco Customer Churn Dataset** (Kaggle) — 7,043 customer records with 21 fields covering demographics, services subscribed (phone, internet, streaming), contract type, payment method, monthly charges, total charges, tenure (months active), and churn status (Yes/No).
Source: https://www.kaggle.com/datasets/blastchar/telco-customer-churn

## Tools Used

Microsoft Power BI Desktop — Power Query for data cleaning, DAX measures for KPI calculations, and an interactive retention dashboard with slicers.

## Repository Structure

```
├── README.md
├── Customer_Churn_Analysis.pbix          # Full Power BI workbook with dashboard
├── Customer_Churn_Analysis_Report.pdf    # Written insights & recommendations report
└── screenshots/
    ├── dashboard_overview.png
    ├── dashboard_filtered.png
    ├── data_loading.png
    ├── power_query_cleaning.png
    ├── calculated_columns.png
    └── dax_measures.png
```

## Data Cleaning Steps (Power Query)

- Fixed `TotalCharges` column: stored as text due to blank values for 0-tenure customers — replaced nulls with 0, converted to Decimal Number
- Converted `SeniorCitizen` from integer (0/1) to readable text (No/Yes) for cleaner chart labels
- Removed duplicate `customerID` rows
- Removed blank rows
- Renamed query from default CSV name to `TelcoChurn` for clean DAX referencing

## Calculated Columns & DAX Measures Added

**Calculated Columns:**
- `ChurnFlag` — 1/0 numeric version of Churn for DAX aggregation
- `SignupDate` — back-calculated from tenure using `EDATE(TODAY(), -tenure)`
- `CohortMonth` — formatted signup date as "MMM-YYYY" for cohort grouping
- `TenureGroup` — SWITCH buckets: 0–12, 13–24, 25–48, 49+ months

**DAX Measures:**
- `Total Customers`, `Churned Customers`, `Churn Rate %`, `Retention Rate %`
- `Avg Tenure Months`, `Avg Monthly Charges`

## Key Findings

| KPI | Value |
|-----|-------|
| Total Customers | 7,043 |
| Churned Customers | 1,869 |
| **Churn Rate** | **26.54%** |
| **Retention Rate** | **73.46%** |
| Avg Tenure | 32.4 months |
| Avg Monthly Charges | $64.76 |

**Contract type** is the strongest churn predictor — month-to-month customers churn at ~42% vs ~3% for two-year contracts. **New customers** (0–12 months) show the highest churn rate. **Fiber optic** customers churn more than DSL despite being the premium tier. **Electronic check** users churn at the highest rate of any payment method.

## Recommendations

1. Convert month-to-month customers to annual contracts with targeted incentives
2. Build a 90-day onboarding program for new customers (highest risk window)
3. Investigate and fix the fiber optic churn problem — premium customers should not be the most at-risk
4. Run an auto-pay migration campaign targeting electronic check and mailed check users
5. Create a high-risk customer early-warning system based on the 4 churn predictors
6. Track cohort churn monthly in Power BI as an ongoing early-warning KPI

Full analysis, charts, and detailed recommendations are in `Customer_Churn_Analysis_Report.pdf`.

## Author

Naredla Poojitha — Data Science & Analytics Intern
