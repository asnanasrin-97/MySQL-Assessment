# E-Commerce Customer Churn Analysis (MySQL)

A SQL project that cleans, transforms and analyses e-commerce customer data to understand **why customers churn** and which groups are most at risk. The goal is to give businesses actionable insights for targeted retention strategies.

## Problem Statement

E-commerce businesses need to understand churn patterns to keep customers satisfied and stay profitable. Using historical transactional data, this project looks at customer attributes such as tenure, preferred payment mode, satisfaction score, distance from the warehouse and purchase behaviour to uncover the drivers of churn.

## Tools Used

- MySQL 8.x
- MySQL Shell for VS Code / MySQL Workbench (any MySQL client works)

## Dataset

- Source: E-commerce customer churn dataset provided with the assignment (CSV)
- Database: `ecomm`
- Main table: `customer_churn` (one row per customer)

| Column | Description |
|---|---|
| CustomerID | Unique customer ID |
| Churn | 1 = churned, 0 = active |
| Tenure | Months with the platform |
| PreferredLoginDevice | Device used to log in |
| CityTier | City tier (1, 2, 3) |
| WarehouseToHome | Distance from warehouse to home |
| PreferredPaymentMode | Preferred way of paying |
| Gender | Customer gender |
| HourSpendOnApp | Hours spent on the app |
| NumberOfDeviceRegistered | Devices registered |
| PreferedOrderCat | Preferred order category |
| SatisfactionScore | Satisfaction rating |
| MaritalStatus | Marital status |
| NumberOfAddress | Saved addresses |
| Complain | 1 = complained in the last month |
| OrderAmountHikeFromlastYear | Order amount increase vs. last year |
| CouponUsed | Coupons used |
| OrderCount | Orders placed |
| DaySinceLastOrder | Days since last order |
| CashbackAmount | Cashback received |

## Project Structure

```
.
├── ecommerce_churn_analysis.sql   # Full script: cleaning, transformation, analysis
└── README.md
```

## How to Run

1. Create the database and the empty table `customer_churn` in `ecomm`.
2. Import the dataset CSV into `customer_churn`. Blank cells must be loaded as `NULL` (use `NULLIF(col, '')` with `LOAD DATA`, or convert `''` to `NULL` after importing).
3. Open `ecommerce_churn_analysis.sql` and run it section by section.

## What the Script Does

### 1. Data Cleaning
- Filled missing values with the **mean** (rounded) for `WarehouseToHome`, `HourSpendOnApp`, `OrderAmountHikeFromlastYear`, `DaySinceLastOrder`.
- Filled missing values with the **mode** for `Tenure`, `CouponUsed`, `OrderCount`.
- Removed outliers: rows where `WarehouseToHome > 100`.
- Standardised labels:
  - `Phone` to `Mobile Phone` in `PreferredLoginDevice`
  - `Mobile` to `Mobile Phone` in `PreferedOrderCat`
  - `COD` to `Cash on Delivery` and `CC` to `Credit Card` in `PreferredPaymentMode`

### 2. Data Transformation
- Renamed `PreferedOrderCat` to `PreferredOrderCat` and `HourSpendOnApp` to `HoursSpentOnApp`.
- Created `ComplaintReceived` (Yes/No) from `Complain`.
- Created `ChurnStatus` (Churned/Active) from `Churn`.
- Dropped the original `Churn` and `Complain` columns.

### 3. Data Exploration and Analysis
Queries answering questions such as:
- Count of churned vs. active customers
- Average tenure and total cashback of churned customers
- Percentage of churned customers who complained
- City tier with the most churned Laptop & Accessory customers
- Most preferred payment mode among active customers
- Total order amount hike for single customers who prefer mobile phones
- Average devices registered for UPI users
- City tier with the most customers
- Gender that used the most coupons
- Customers and maximum app hours per order category
- Total orders for credit-card customers with the top satisfaction score
- Average satisfaction score of customers who complained
- Order categories among customers with more than 5 coupons
- Top 3 order categories by average cashback
- Payment modes with average tenure of 10 months and more than 500 orders
- Churn breakdown by distance category (Very Close, Close, Moderate, Far)
- Order details of married, City Tier 1 customers with above-average order counts
- A `customer_returns` table with return and refund data, joined to churned customers who complained

## SQL Concepts Practised

`UPDATE` and `DELETE`, user variables, `ALTER TABLE` (add, rename, drop), `CASE WHEN`, aggregate functions, `GROUP BY` / `HAVING`, subqueries, `JOIN`, `CREATE TABLE` and `INSERT`.

## Key Insights

> Fill this in after running the queries, for example:
> - Overall churn rate: _X%_
> - Highest-churn city tier: _Tier N_
> - Relationship between complaints and churn: _..._
> - Relationship between distance from the warehouse and churn: _..._
> - Suggested retention actions: _..._

## Author

_Your name_ · _LinkedIn / email (optional)_
