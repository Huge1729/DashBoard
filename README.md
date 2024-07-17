# Credit Card Weekly Dashboard

## Project Overview

This project aims to develop a comprehensive weekly credit card dashboard using Power BI that provides real-time insights into key performance metrics and trends. The dashboard enables stakeholders to monitor and analyze credit card operations effectively, facilitating data-driven decision-making and operational efficiency.

## Features

- Overall revenue is 57M
- Total interest is 8M
- Total transaction amount is 46M
- Male customers are contributing more in revenue 31M, females 26M
- Blue & Silver credit cards are contributing to 93% of overall transactions
- TX, NY & CA is contributing to 68%
- Overall Activation rate is 57.5%
- Overall Delinquent rate is 6.06%

## Technology Stack

- **Data Visualization**: Power BI
- **Data Source**: CSV, Excel, Postgres Databases
- **Scripting**: DAX (Data Analysis Expressions)
- **Deployment**: Power BI Service



### Steps

- Prepare CSV file
- Create tables in SQL
- Import CSV file into SQLt
- Build the Dashboard
- DAX Queries
- For AgeGroup Column
 ```
AgeGroup = SWITCH(
TRUE(),
'public cust_detail'[customer_age] < 30, "20-30",
'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
'public cust_detail'[customer_age] >= 60, "60+",
"unknown"
)
```

- For Income Category Column
```
IncomeGroup = SWITCH(
TRUE(),
'public cust_detail'[income] < 35000, "Low",
'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
'public cust_detail'[income] >= 70000, "High",
"unknown"
)
```
- For Week Number Count Column 
```
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

- For Revenue Column
 ```
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
```
- for Total week wise Revenue Column
```
Current_week_Reveneue = CALCULATE(
SUM('public cc_detail'[Revenue]),
FILTER(
ALL('public cc_detail'),
'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))

Previous_week_Reveneue = CALCULATE(
SUM('public cc_detail'[Revenue]),
FILTER(
ALL('public cc_detail'),
'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))
```
