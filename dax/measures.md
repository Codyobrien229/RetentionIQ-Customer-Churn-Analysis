# RetentionIQ DAX Measures

This file documents the primary DAX measures and calculated columns used in the RetentionIQ Power BI dashboard.

## Core Measures

### Total Customers
```DAX
Total Customers =
DISTINCTCOUNT(Customers[CustomerID])
```

### Churned Customers
```DAX
Churned Customers =
CALCULATE(
    [Total Customers],
    Customers[Churn] = "Yes"
)
```

### Churn Rate
```DAX
Churn Rate =
DIVIDE(
    [Churned Customers],
    [Total Customers]
)
```

### Monthly Revenue at Risk
```DAX
Monthly Revenue at Risk =
CALCULATE(
    SUM(Customers[MonthlyCharges]),
    Customers[Churn] = "Yes"
)
```

### Average Monthly Charge
```DAX
Avg Monthly Charge =
AVERAGE(Customers[MonthlyCharges])
```

## High-Risk Customer Measures

High-risk customers are defined as active month-to-month customers with a satisfaction score of 3 or lower who also have either at least two support calls in the last 12 months or tenure of 12 months or less.

### High-Risk Customers
```DAX
High-Risk Customers =
CALCULATE(
    [Total Customers],
    Customers[Churn] = "No",
    Customers[ContractType] = "Month-to-Month",
    Customers[SatisfactionScore] <= 3,
    FILTER(
        Customers,
        Customers[SupportCallsLast12Months] >= 2
            || Customers[TenureMonths] <= 12
    )
)
```

### Average Monthly Charge — High Risk
```DAX
Avg Monthly Charge - High Risk =
CALCULATE(
    AVERAGE(Customers[MonthlyCharges]),
    Customers[Churn] = "No",
    Customers[ContractType] = "Month-to-Month",
    Customers[SatisfactionScore] <= 3,
    FILTER(
        Customers,
        Customers[SupportCallsLast12Months] >= 2
            || Customers[TenureMonths] <= 12
    )
)
```

### Average Tenure — High Risk
```DAX
Avg Tenure - High Risk =
CALCULATE(
    AVERAGE(Customers[TenureMonths]),
    Customers[Churn] = "No",
    Customers[ContractType] = "Month-to-Month",
    Customers[SatisfactionScore] <= 3,
    FILTER(
        Customers,
        Customers[SupportCallsLast12Months] >= 2
            || Customers[TenureMonths] <= 12
    )
)
```

### Average Satisfaction — High Risk
```DAX
Avg Satisfaction - High Risk =
CALCULATE(
    AVERAGE(Customers[SatisfactionScore]),
    Customers[Churn] = "No",
    Customers[ContractType] = "Month-to-Month",
    Customers[SatisfactionScore] <= 3,
    FILTER(
        Customers,
        Customers[SupportCallsLast12Months] >= 2
            || Customers[TenureMonths] <= 12
    )
)
```

## Customer Segmentation Columns

### Tenure Band
Groups customers into tenure ranges for retention analysis.

```DAX
Tenure Band =
SWITCH(
    TRUE(),
    Customers[TenureMonths] <= 12, "0–12 Months",
    Customers[TenureMonths] <= 24, "13–24 Months",
    Customers[TenureMonths] <= 36, "25–36 Months",
    Customers[TenureMonths] <= 48, "37–48 Months",
    Customers[TenureMonths] <= 60, "49–60 Months",
    "61–72 Months"
)
```

### Tenure Band Sort
Provides the numeric sort order for the tenure categories.

```DAX
Tenure Band Sort =
SWITCH(
    TRUE(),
    Customers[TenureMonths] <= 12, 1,
    Customers[TenureMonths] <= 24, 2,
    Customers[TenureMonths] <= 36, 3,
    Customers[TenureMonths] <= 48, 4,
    Customers[TenureMonths] <= 60, 5,
    6
)
```

### Monthly Charge Band
Groups customers by monthly spending level.

```DAX
Monthly Charge Band =
SWITCH(
    TRUE(),
    Customers[MonthlyCharges] < 40, "Under $40",
    Customers[MonthlyCharges] < 60, "$40–59",
    Customers[MonthlyCharges] < 80, "$60–79",
    Customers[MonthlyCharges] < 100, "$80–99",
    "$100+"
)
```

### Monthly Charge Band Sort
Provides the numeric sort order for monthly charge categories.

```DAX
Monthly Charge Band Sort =
SWITCH(
    TRUE(),
    Customers[MonthlyCharges] < 40, 1,
    Customers[MonthlyCharges] < 60, 2,
    Customers[MonthlyCharges] < 80, 3,
    Customers[MonthlyCharges] < 100, 4,
    5
)
```
