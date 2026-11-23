# Purchasing & Budget Analytics Dashboard | Power BI

## Project Overview

I developed an interactive Power BI dashboard to analyze purchasing activity, departmental budgets, vendor spending, and payment processing performance.

The objective of this project was to transform purchasing and financial data into meaningful insights that support budget monitoring, vendor management, and operational decision-making.

The dashboard consists of three report pages:

1. **Purchasing & Budget Performance** – Analyzes organizational spending, budget utilization, and vendor spending concentration.
2. **Vendor Details** – Provides detailed purchasing information by vendor, including individual purchase orders.
3. **Payment Performance** – Evaluates payment processing efficiency and identifies potential delays.

## Tools & Technologies

- **Power BI Desktop:** Interactive dashboard development
- **DAX:** Calculated measures and financial KPIs
- **Power Query:** Data preparation and transformation
- **Data Modeling:** Relational tables, cardinality, and filter relationships
- **Data Visualization:** KPI cards, bar charts, line charts, donut charts, and tables
- **Data Validation:** Duplicate checks, missing-value checks, and financial reconciliation

## Data Modeling & Relationships

I created a relational data model connecting seven tables to analyze purchasing, budget, and payment information across multiple business dimensions.

### Data Tables

| Table | Purpose |
|---|---|
| FactPurchasesTable | Stores purchase orders, purchasing amounts, vendor IDs, and department IDs |
| FactPaymentsTable | Contains payment transactions, payment amounts, dates, and processing times |
| FactBudgetTable | Stores departmental budget allocations |
| DimVendorTable | Contains vendor names and unique vendor IDs |
| DimDepartmentTable | Contains department information |
| DimDateTable | Supports date-based purchasing analysis |
| DimMonthTable | Supports monthly reporting and budget comparisons |

### Relationships Created

| Tables Connected | Matching Columns | Business Purpose |
|---|---|---|
| DimVendorTable → FactPurchasesTable | VendorID | Connect purchase orders to vendor names and analyze supplier spending |
| DimDepartmentTable → FactPurchasesTable | DepartmentID | Analyze purchasing activity across departments |
| DimDepartmentTable → FactBudgetTable | DepartmentID | Compare spending against departmental budgets |
| DimDateTable → FactPurchasesTable | Date / OrderDate | Analyze purchasing trends over time |
| DimMonthTable → FactBudgetTable | MonthStart / BudgetMonth | Align monthly budget allocations with reporting periods |
| DimMonthTable → DimDateTable | MonthStart | Connect calendar dates with monthly reporting periods |
| FactPurchasesTable ↔ FactPaymentsTable | PurchaseOrderID | Associate purchase orders with payment transactions |

### Why I Created These Relationships

Instead of combining all information into one large table, I used relationships to connect different datasets through shared identifiers.

For example, `FactPurchasesTable` contains VendorID, while `DimVendorTable` contains the corresponding vendor names.

By connecting the tables through VendorID, I was able to display vendor names alongside purchase orders without manually adding vendor names to every transaction.

Similarly, connecting purchase orders to payment records through PurchaseOrderID allowed me to analyze purchasing and payment activity together.

This approach supported interactive filtering, more organized data analysis, and reusable DAX calculations.

*Note: The purchase-to-payment relationship should be validated against the data's actual payment cardinality before treating it as a finalized production model.*

<img width="568" height="384" alt="image" src="https://github.com/user-attachments/assets/aa00da56-0527-4f7f-a9e0-038565706552" />


## Dashboard Pages

### 1. Purchasing & Budget Performance

This page provides an overview of purchasing activity and departmental budget performance.

**Key Performance Indicators:**

- Total Spend
- Total Budget
- Budget Variance
- Budget Used %
- Top 5 Vendor Spend %

**Dashboard Features:**

- Department-level spending and budget comparison
- Conditional formatting to highlight departments exceeding their budgets
- Monthly spending versus budget trends
- Top five vendors ranked by purchasing spend
- Interactive month filtering

**Key Findings:**

| Metric | Result |
|---|---:|
| Total Spend | Approximately $1.12M |
| Total Budget | Approximately $1.07M |
| Budget Variance | Approximately -$50.65K |
| Budget Used % | 104.75% |
| Top 5 Vendor Spend % | 67.69% |

Overall spending exceeded the allocated budget by approximately 4.75%.

The top five vendors accounted for 67.69% of purchasing spend, highlighting vendor spending concentration.

<img width="658" height="371" alt="image" src="https://github.com/user-attachments/assets/0cb0139f-0f21-4616-b0f4-fd40337914a3" />


### 2. Vendor Details

This page allows users to investigate individual vendors and their associated purchase orders.

**Dashboard Features:**

- Total Spend KPI
- Total Purchase Orders KPI
- Vendor Name slicer
- Purchase Category slicer
- Purchase order transaction details
- Drill-through navigation from the Main Dashboard

The purchase order table includes Vendor Name, PurchaseOrderID, OrderDate, and Purchase Amount.

By selecting a vendor, users can examine purchasing activity without creating separate reports for each supplier.

This page supports questions such as:

- How much has been spent with a particular vendor?
- How many purchase orders were placed?
- Which purchasing categories contribute to vendor spending?
- When were purchases made, and what were their amounts?

<img width="641" height="374" alt="image" src="https://github.com/user-attachments/assets/73fe2482-782e-4a20-8f31-8c9a667546ee" />

### 3. Payment Performance

This page evaluates payment processing efficiency and identifies opportunities for operational improvement.

**Key Performance Indicators:**

- Total Payments
- Average Days to Pay
- Payments Over 30 Days %

**Dashboard Features:**

- Payment processing time breakdown
- Average payment days by department
- Average payment days by vendor
- Monthly payment trends
- Interactive department filtering

**Key Findings:**

| Metric | Result |
|---|---:|
| Total Payments | $973,194.79 |
| Average Days to Pay | Approximately 42 days |
| Payments Over 30 Days | 68.29% |
| Payments Taking Over 30 Days | 140 |
| Payments Within 30 Days | 65 |

The analysis showed that 68.29% of recorded payments took more than 30 days to process.

These findings suggest an opportunity to investigate payment processing delays and evaluate whether improvements to internal workflows could reduce processing times.

<img width="724" height="391" alt="image" src="https://github.com/user-attachments/assets/da09c8e4-bb6e-4057-b6f7-87707d400007" />


## DAX Measures

I developed DAX measures to calculate purchasing, budget, vendor, and payment performance indicators.

Examples include:

| DAX Measure | Purpose |
|---|---|
| Total Spend | Calculates total purchasing expenditures |
| Total Budget | Calculates allocated budgets |
| Budget Variance | Measures the difference between budget and spending |
| Budget Used % | Calculates budget utilization |
| Total Purchase Orders | Counts purchase orders |
| Top 5 Vendor Spend % | Measures spending concentration among the top five vendors |
| Total Payments | Calculates total payment amounts |
| Average Days to Pay | Measures average payment processing time |
| Payments Over 30 Days % | Calculates the proportion of payments exceeding 30 days |

These measures respond to report filters and allow users to analyze different vendors, departments, and reporting periods.

## Data Quality Validation & Troubleshooting

To improve the reliability of the dashboard, I performed several data quality and validation checks.

### Validation Performed

- **Duplicate PaymentIDs:** Confirmed no duplicate payment IDs in the tested context.
- **Missing Payment Data:** Checked required payment fields for missing values.
- **Unmatched Payments:** Checked whether payment records were associated with purchase orders.
- **Payment Reconciliation:** Confirmed monthly payment totals reconciled to $973,194.79.
- **Interactive Filtering:** Tested vendor and department filters to verify that KPIs and visualizations updated correctly.

### Troubleshooting Example: Missing Purchase Order IDs

During dashboard development, I discovered that certain purchase order IDs were not appearing in the Vendor Details table, even though the transactions existed in the purchasing dataset.

I investigated the issue by reviewing the source data, testing DAX calculations, checking table relationships, and examining the fields used in the report visual.

I identified that the report was referencing PurchaseOrderID from `FactPaymentsTable` instead of `FactPurchasesTable`.

Because some purchase orders did not have corresponding payment records, those IDs were not displayed as expected.

**Resolution:** I updated the visual to use PurchaseOrderID from FactPurchasesTable, ensuring the purchasing report displayed the correct purchase order identifiers.

This experience reinforced the importance of selecting the correct fact table, understanding data relationships, and validating report outputs against source records.

## Skills Demonstrated

- Power BI Dashboard Development
- DAX Measures and KPI Development
- Relational Data Modeling
- Financial and Purchasing Analysis
- Budget Variance Analysis
- Vendor Spend Analysis
- Payment Performance Analysis
- Data Quality Validation
- Data Troubleshooting
- Interactive Filtering and Drill-Through Reporting
- Data Visualization and Business Intelligence


## Conclusion

This project strengthened my ability to build interactive business intelligence reports, connect multiple datasets through relational data modeling, develop financial KPIs using DAX, and validate analytical results.

Through this project, I gained practical experience troubleshooting data model and visualization issues while transforming purchasing and payment information into actionable business insights.

The final dashboard demonstrates how Power BI can support purchasing oversight, budget monitoring, vendor analysis, and payment performance evaluation.
