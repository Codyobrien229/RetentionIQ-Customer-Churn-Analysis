# RetentionIQ | Customer Retention & Churn Analysis

**Power BI | Power Query | DAX | Customer Segmentation | Churn Analysis**

RetentionIQ is an interactive Power BI analysis of **8,000 telecommunications customers** designed to identify key churn drivers, high-risk customer segments, and actionable retention opportunities.

> **Note:** This project uses a synthetic dataset created for portfolio and educational purposes. No real customer information is used.

---

## Dashboard

### Churn Overview

![RetentionIQ Churn Overview](images/churn_overview.png)

The Churn Overview provides an executive-level view of overall customer churn and examines how churn varies across contract type, internet service, tenure, and monthly charges.

### Customer Segmentation

![RetentionIQ Customer Segmentation](images/customer_segmentation.png)

The Customer Segmentation page provides deeper analysis of customer risk patterns using interactive filters, high-risk customer KPIs, payment and support analysis, customer segmentation, and value/risk comparisons.

---

## Key Findings

- **30.4% overall churn rate** — 2,435 of 8,000 customers churned.

- **Month-to-month customers had a 43.0% churn rate**, compared with 18.2% for one-year contracts and 10.6% for two-year contracts.

- **Customers within their first 12 months had a 43.0% churn rate**, making early customer tenure a major retention opportunity.

- Customers paying **$100+ per month had a 37.4% churn rate**, compared with 18.6% among customers paying under $40.

- The combination of **0–12 months tenure and $100+ monthly charges had a 48.9% churn rate**, the highest-risk tenure/charge segment identified.

- Customers with **6 support calls had a 50.0% churn rate**, showing a strong association between repeated support interactions and customer churn.

- **Electronic Check customers had a 35.1% churn rate**, the highest among the payment methods analyzed.

---

## Business Recommendations

1. **Prioritize early-tenure retention**  
   Develop proactive onboarding and customer check-ins during the first 12 months, when churn is highest.

2. **Focus on high-charge, early-tenure customers**  
   Customers with 0–12 months of tenure and monthly charges of $100 or more represent one of the highest-churn segments identified.

3. **Use repeated support activity as a retention signal**  
   Customers requiring frequent support interactions may benefit from proactive outreach before service issues contribute to churn.

4. **Encourage longer-term contracts**  
   Evaluate incentives that encourage month-to-month customers to transition to one- or two-year agreements.

5. **Investigate Electronic Check customers further**  
   Additional analysis could determine whether billing friction, customer characteristics, or other factors contribute to the higher churn observed within this payment group.

---

## Business Problem

A telecommunications company is experiencing customer churn and wants to better understand which customers are leaving, what factors are associated with churn, and which customer segments should be prioritized for retention efforts.

The analysis was designed to answer several business questions:

- How significant is churn across the overall customer base?
- Which contract types experience the highest churn?
- How does customer tenure relate to churn?
- Are customers with higher monthly charges more likely to churn?
- Are repeated support interactions associated with increased churn?
- Which customer segments may warrant additional retention attention?

The goal was to transform customer-level data into an interactive Power BI dashboard that allows decision-makers to quickly identify important churn patterns and retention opportunities.

---

## Dataset

The analysis uses a synthetic telecommunications customer dataset containing:

- **8,000 customers**
- **23 fields**
- Customer demographics
- Contract information
- Customer tenure
- Internet and additional services
- Monthly and total charges
- Payment method
- Support activity
- Satisfaction score
- Churn status

Each row represents one fictional telecommunications customer.

---

## Data Preparation

Data preparation was completed using **Power Query** before building the Power BI report.

The dataset intentionally included several data-quality issues to simulate a realistic analytics workflow.

Cleaning and transformation included:

- Standardizing inconsistent **Contract Type** values
- Trimming leading and trailing spaces from **Payment Method**
- Identifying missing **Total Charges** values
- Imputing missing Total Charges using Monthly Charges and customer tenure
- Validating and correcting column data types
- Checking Customer IDs for duplicates
- Preparing the cleaned dataset for analysis and visualization

---

## DAX & Data Modeling

DAX was used to create the KPIs, segmentation fields, and business logic used throughout the dashboard.

Core measures included:

- Total Customers
- Churned Customers
- Churn Rate
- Monthly Revenue at Risk
- Average Monthly Charge
- High-Risk Customers
- Average Monthly Charge — High Risk
- Average Tenure — High Risk
- Average Satisfaction — High Risk

Calculated columns were also created to segment customers by:

- **Tenure Band**
- **Monthly Charge Band**

Numeric sort columns were created to ensure these segments appeared in the correct business order within dashboard visuals.

The complete DAX used in the project is documented here:

[`dax/measures.md`](dax/measures.md)

---

## High-Risk Customer Segmentation

A rule-based customer segment was created to identify active customers who may warrant additional retention attention.

A customer was classified as **High Risk** when the customer:

- Had not already churned
- Had a month-to-month contract
- Had a satisfaction score of 3 or lower
- Had at least 2 support calls in the previous 12 months **or** had tenure of 12 months or less

This identified a cohort of **286 high-risk customers**.

Within this group:

- **Average Monthly Charge:** $79.26
- **Average Tenure:** 24.1 months
- **Average Satisfaction Score:** 2.86 / 5

> This segmentation is based on defined business rules and descriptive analysis. It is **not a predictive churn or machine-learning model**.

---

## Dashboard Features

The Power BI report includes:

- Executive KPI cards
- Interactive customer segmentation slicers
- Churn analysis by contract type
- Churn analysis by internet service
- Tenure-based churn analysis
- Monthly charge analysis
- Payment method analysis
- Support call analysis
- Customer value/risk scatter analysis
- Tenure and monthly-charge risk segmentation heatmap
- Conditional formatting
- Reference lines
- Cross-filtering between visuals
- Rule-based high-risk customer KPIs
- Retention recommendations

---

## Tools & Skills Demonstrated

### Power BI
- Dashboard development
- KPI design
- Interactive slicers
- Cross-filtering
- Conditional formatting
- Reference lines
- Scatter plots
- Matrix/heatmap visualization
- Executive dashboard design

### Power Query
- Data cleaning
- Data transformation
- Missing-value handling
- Text standardization
- Data-type validation

### DAX
- Measures
- Calculated columns
- `CALCULATE`
- `FILTER`
- `DIVIDE`
- `DISTINCTCOUNT`
- `SWITCH`
- Customer segmentation
- KPI development

### Data Analysis
- Customer churn analysis
- Customer segmentation
- Retention analysis
- KPI development
- Business insight development
- Data visualization
- Business recommendations

---

## Repository Structure

```text
RetentionIQ-Customer-Churn-Analysis/
│
├── README.md
│
├── data/
│   └── RetentionIQ_Customer_Churn_Data.csv
│
├── dax/
│   └── measures.md
│
└── images/
    ├── churn_overview.png
    └── customer_segmentation.png
```

---

## Next Steps

Potential extensions of the project include:

- Incorporating customer lifetime value into retention prioritization
- Analyzing customer behavior and churn longitudinally with time-series data
- Evaluating retention campaign performance
- Conducting deeper analysis of customer support interactions
- Expanding customer segmentation using additional behavioral characteristics
- Comparing retention strategies across customer groups
