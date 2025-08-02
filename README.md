📊 Project Title: Supply Chain Analytics – Puscha Health
---

Author: Tran Thi Ngoc Quyen


Date: 2025-05-01


Tools Used: Power BI
***
📑 Table of Contents

📌 Background & Overview
---

📂 Dataset Description & Data Structure


🧠 Design Thinking Process


📊 Key Insights & Visualizations


🔎 Final Conclusion & Recommendations
***
📌 Background & Overview
---

📖 What is this project about?


This project analyzes purchasing performance and vendor-related risks for a fictional bicycle manufacturing company – Adventure Works Cycles – using Power BI. The objectives are:


✔️ Evaluate vendor performance based on cost, delivery timeliness, and rejection rates


✔️ Identify supply and delivery risks such as late shipments and quantity mismatches


✔️ Monitor purchasing health through trends in lead time, cost, and risk exposure


✔️ Optimize ordering decisions by analyzing order frequency and small-quantity orders


✔️ Provide actionable insights through Power BI dashboards

👤 Who is this project for?


✔️ Data analysts & supply chain analysts


✔️ Procurement and vendor management teams


✔️ Business leaders & operations managers in manufacturing companies
***
📂 Dataset Description & Data Structure
---

📌 Data Source


Source: AdventureWorks – a sample dataset for a fictional bicycle manufacturing company


Size: Multiple tables with thousands of rows and dozens of columns. Exact row and column counts vary by table


Format: .pbix (Power BI Desktop File)

📊 Data Structure & Relationships


1️⃣ Tables Used:


✔️ Dim_Vedor


✔️ DimDate


✔️ Fact_PurchaseOrder


✔️ OrdersPerDay


✔️ Purchasing_OrderHeader


✔️ Purchasing_ProductVendor


✔️ Purchasing_Vendor

2️⃣ Table Schema & Data Snapshot

 ✔️ Dataset & Tables Overview

 | Table Name             | Description |
|------------------------|-------------|
| `MeasureTable`         | Contains calculated measures such as total orders, on-time delivery %, and vendor health score. Helps in organizing DAX and simplifying visuals. |
| `*Product_Inventory`   | Inventory data of products by location. Used to analyze inventory levels and stock movement in relation to purchase orders. |
| `Dim_Vendor`           | Dimension table with detailed information about vendors. Linked to `Fact_PurchaseOrder` for vendor-based analysis. |
| `DimDate`              | Standardized date table used to enable time-series analysis. Connected with `ModifiedDate` from the purchase order table. |
| `Fact_PurchaseOrder`   | The main fact table containing purchase order data including product, quantity, vendor, cost, and timestamps. Central to all procurement KPIs. |
| `OrdersPerDay`         | Aggregated table showing the number of orders per day. Supports trend analysis and workload evaluation. |
| `Parameter`            | Table with slicer/parameter values used in Power BI reports. Useful for filtering by year, vendor, or performance indicators. |



Table 1: Dim_Vendor


<img width="1164" height="470" alt="image" src="https://github.com/user-attachments/assets/b3432533-92c8-4fc1-99ad-c889fb14be92" />


| Column Name      | Data Type     | Description                                                       |
|------------------|---------------|-------------------------------------------------------------------|
| VendorKey        | Whole Number  | Unique identifier for each vendor (from BusinessEntityID)         |
| VendorName       | Text          | Name of the vendor                                                 |
| CreditRating     | Whole Number  | Credit score indicating vendor reliability                         |
| PreferredStatus  | True/False      | Flag indicating preferred vendor (PreferredVendorStatus)           |
| IsActive         | True/False      | Vendor activity status (True: Active)                              |

Table 2: DimDate


<img width="820" height="235" alt="image" src="https://github.com/user-attachments/assets/965d38b1-1819-447a-860e-8c55dcfd4072" />

| Column Name      | Data Type | Description                                |
|------------------|-----------|--------------------------------------------|
| Date             | Date      | Full date value                            |
| Year             | Whole Number  | Year component of the date                 |
| Month            | Whole Number   | Month number (1–12)                        |
| Day              | Whole Number   | Day of the month (1–31)                    |
| MonthName        | Text      | Abbreviated month name (e.g., Jan, Feb...) |
| MonthNameFull    | Text      | Full month name (e.g., January, February)  |
| MonthYear        | Text      | Year and month in YYYY-MM format           |
| Quarter          | Text      | Quarter of the year (Q1–Q4)                |
| YearMonthSort    | Whole Number   | Sortable key in format YYYYMM              |

Table 3: Fact_PurchaseOrder
<img width="2048" height="343" alt="244bda8a-02a9-4c6b-9d85-57d0295856d7" src="https://github.com/user-attachments/assets/503f5abc-f52e-4303-9264-1d883d283826" />
<img width="2048" height="343" alt="74e64b35-33d9-4d28-bf5b-d40521451753" src="https://github.com/user-attachments/assets/a80e20b6-961d-48c6-aad5-bd91e94746f4" />
<img width="777" height="234" alt="400e99d6-b84e-4295-b821-655e70f2f3bf" src="https://github.com/user-attachments/assets/2c223e57-63d3-4990-a5aa-0819242e413b" />

<details>
  <summary>📊 Click để xem bảng <strong>PurchaseOrderDetail</strong> (Full Schema)</summary>

  
| Column Name             | Data Type | Description                                                       |
|--------------------------|-----------|-------------------------------------------------------------------|
| PurchaseOrderID          | INT       | ID of the purchase order                                          |
| PurchaseOrderDetailID    | INT       | Line item ID within the order                                     |
| DueDate                  | DATE      | Expected delivery date                                            |
| OrderQty                 | INT       | Quantity ordered                                                  |
| ProductID                | INT       | Product identifier                                                |
| UnitPrice                | FLOAT     | Price per unit                                                    |
| LineTotal                | FLOAT     | Total cost for the line item                                      |
| ReceivedQty              | INT       | Quantity received                                                 |
| RejectedQty              | INT       | Quantity rejected                                                 |
| StockedQty               | INT       | Quantity stocked                                                  |
| ModifiedDate             | DATE      | Last modification date                                            |
| YearMonth                | TEXT      | Month of order in format YYYY-MM                                  |
| Gap                      | INT       | Difference in days between expected & actual                      |
| OnTimeDeliveryRate       | INT       | Binary flag or score for on-time delivery                         |
| OnTimeDeliveryScore      | INT       | Delivery punctuality score                                        |
| RejectedRate             | FLOAT     | Percentage of items rejected                                      |
| RejectedRateScore        | INT       | Score based on rejection rate                                     |
| LeadTime                 | INT       | Time (in days) between order and receipt                          |
| LeadTimeScore            | INT       | Score based on lead time                                          |
| PurchasingHealthScore    | INT       | Composite score measuring order quality                           |
| IsLateDelivery           | BOOLEAN   | 1 if late delivery, else 0                                        |
| Status                   | INT       | Status of the order                                               |
| VendorID                 | INT       | ID of the vendor                                                  |
| ShipMethodID             | INT       | Shipping method identifier                                        |
| OrderDate                | DATE      | Date the order was placed                                         |
| Lead Time                | INT       | Number of days between order and delivery                         |
| IsOnTime                 | BOOLEAN   | Indicates whether the order was delivered on time                 |
| IsQuantityMismatch       | BOOLEAN   | Flag for quantity mismatch between order & receipt                |
| DeliveryStatus           | TEXT      | Label for delivery (e.g., "On Time", "Late")                      |
| StockoutQty              | INT       | Quantity leading to stockout                                      |
| Order Month              | TEXT      | Month in which order was placed (short format)                    |
| OrderDateOnly            | DATE      | Order date (without time component)                               |

</details>

Table 4: OrdersPerDay


<img width="239" height="130" alt="image" src="https://github.com/user-attachments/assets/9d72b618-8059-4afb-8565-07d73c6fac85" />



| Column Name     | Data Type | Description                                      |
|------------------|-----------|--------------------------------------------------|
| OrderDateOnly    | Date      | Order date (without time component)             |
| DailyOrders      | Whole Number   | Number of purchase orders placed on that date   |


Table 5: Purchasing_OrderHeader


<img width="1205" height="152" alt="image" src="https://github.com/user-attachments/assets/935a4c20-17b9-4b08-b3f5-f8cbebdef12f" />

| Column Name       | Data Type | Description                                           |
|-------------------|-----------|-------------------------------------------------------|
| PurchaseOrderID   | INT       | Unique ID of the purchase order                      |
| RevisionNumber    | INT       | Internal version number of the order                 |
| Status            | INT       | Order status code (e.g., 4 = Approved)               |
| EmployeeID        | INT       | ID of the employee who created the order             |
| VendorID          | INT       | ID of the vendor associated with the order           |
| ShipMethodID      | INT       | Shipping method used                                 |
| OrderDate         | DATE      | Date when the order was placed                       |
| ShipDate          | DATE      | Date when the order was shipped                      |
| SubTotal          | FLOAT     | Total amount before tax and freight                  |
| TaxAmount         | FLOAT     | Amount of tax applied                                |
| Freight           | FLOAT     | Freight/shipping cost                                |
| TotalDue          | FLOAT     | Total amount due (SubTotal + Tax + Freight)          |
| ModifiedDate      | DATE      | Last modified date of the order                      |




Table 6: Purchasing_ProductVendor


<img width="1288" height="132" alt="image" src="https://github.com/user-attachments/assets/07ea9cda-f4ea-4ea8-90c6-cd477ff8ea7f" />

| Column Name        | Data Type | Description                                                       |
|---------------------|-----------|-------------------------------------------------------------------|
| ProductID           | INT       | ID of the product                                                 |
| BusinessEntityID    | INT       | ID of the vendor supplying the product                            |
| AverageLeadTime     | INT       | Average number of days between order and delivery                 |
| StandardPrice       | FLOAT     | Standard unit price for the product                               |
| LastReceiptCost     | FLOAT     | Cost from the most recent purchase                                |
| LastReceiptDate     | DATE      | Date when the product was last received                           |
| MinOrderQty         | INT       | Minimum quantity required per order                               |
| MaxOrderQty         | INT       | Maximum quantity allowed per order                                |
| OnOrderQty          | INT       | Quantity currently on order (nullable)                            |
| UnitMeasureCode     | TEXT      | Code for unit of measure (e.g., CTN = Carton)                     |
| ModifiedDate        | DATE      | Last modified date of the record  



Table 7: Purchasing_Vendor


<img width="1191" height="130" alt="image" src="https://github.com/user-attachments/assets/40b5ab75-bd8e-4727-bf97-d43ce88ebe93" />

| Column Name             | Data Type | Description                                                    |
|--------------------------|-----------|----------------------------------------------------------------|
| BusinessEntityID         | INT       | Unique identifier of the vendor (foreign key)                  |
| AccountNumber            | TEXT      | Vendor’s internal account number                               |
| Name                     | TEXT      | Name of the vendor                                              |
| CreditRating             | INT       | Numeric rating of vendor's creditworthiness                    |
| PreferredVendorStatus    | BOOLEAN   | Indicates preferred vendor (1 = Yes, 0 = No)                   |
| ActiveFlag               | BOOLEAN   | Vendor activity status (1 = Active, 0 = Inactive)              |
| PurchasingWebServiceURL  | TEXT      | URL to vendor’s web service (nullable)                         |
| ModifiedDate             | DATE      | Last modified date of the vendor record                        |
| RiskCategory             | TEXT      | Risk level of the vendor (e.g., High, Medium, Low)             |


3️⃣ Data Relationships:

This section describes the relationships between tables in the data model. The connections were established to support accurate filtering, aggregation, and slicing of data across fact and dimension tables.

| From Table (Column)                            | To Table (Column)                                  | Relationship Type | Status  |
|------------------------------------------------|----------------------------------------------------|-------------------|---------|
| `Product_Inventory (LocationID)`              | `Production_Location (LocationID)`                | One-to-One        | Active  |
| `Fact_PurchaseOrder (ModifiedDate)`           | `DimDate (Date)`                                  | Many-to-One       | Active  |
| `Fact_PurchaseOrder (ProductID)`              | `Product_ProductTable (ProductID)`                | Many-to-One       | Active  |
| `Fact_PurchaseOrder (PurchaseOrderID)`        | `Purchasing_OrderHeader (PurchaseOrderID)`        | One-to-One        | Active  |
| `Fact_PurchaseOrder (VendorID)`               | `Dim_Vendor (VendorKey)`                          | Many-to-One       | Active  |
| `Production_WorkOrderRouting (LocationID)`    | `Production_Location (LocationID)`                | Many-to-One       | Active  |
| `Production_WorkOrderRouting (WorkOrderID)`   | `Production_WorkOrder (WorkOrderID)`              | Many-to-One       | Active  |
| `Purchasing_ProductVendor (BusinessEntityID)` | `Purchasing_Vendor (BusinessEntityID)`            | Many-to-One       | Active  |

📌 Notes:
All relationships are active, ensuring smooth data model interactions.
The data model primarily follows a star schema pattern, where Fact_PurchaseOrder acts as the central fact table linked to multiple dimensions.
These relationships are key to enabling efficient drill-downs and cross-filtering in visualizations.

<img width="790" height="420" alt="image" src="https://github.com/user-attachments/assets/18ca4c3c-403b-4673-a639-662bce6f9dc0" />
***


🧠 Design Thinking Process
---


1️⃣ Empathize

Goal: Deeply understand the challenges the business faces in supply chain operations.


Actions Taken:


Analyzed historical data on purchase orders, vendors, and delivery timelines.


Conducted internal interviews with stakeholders (procurement, finance, operations).


Identified key pain points: late deliveries, inconsistent suppliers, and non-optimized costs.

2️⃣ Define Point of View


Goal: Clearly define the problem from the end-user’s perspective.


Problem Statement:


“Operations managers need a clear and effective way to evaluate supplier performance and optimize ordering decisions to reduce delivery risks and ensure financial efficiency in the supply chain.”

3️⃣ Ideate


Goal: Generate possible solutions to address the problem.


Ideas Generated:


Build dashboards to track vendor performance.


Score purchase risks based on historical delivery data.


Identify stable and reliable vendors to prioritize future orders.


Propose data-driven order optimization policies

4️⃣ Prototype and Review


Goal: Build a prototype dashboard and collect feedback.


Actions Taken:


Created Power BI dashboards with key views like “Vendor Effectiveness,” “Purchasing Health,” and “Delivery Risk.”


Presented the prototype to decision-makers and gathered feedback.


Refined the dashboard visuals and analytics logic based on real user input.


***


⚒️ Main Process
---
1️⃣ Data Cleaning & Preprocessing


Performed initial data cleaning using Power Query


Removed missing or duplicate values


Standardized column names and data types


Merged and processed key columns such as VendorID and ProductID


Checked data consistency across related tables


📌 Purpose: To ensure the dataset is clean, consistent, and ready for analysis and modeling.

2️⃣ Exploratory Data Analysis (EDA)


Evaluated vendor performance by delivery time, quantity mismatch, and rejection rate


Identified patterns of late deliveries and low purchasing health scores


Analyzed order volume fluctuations and small quantity frequency


Highlighted suppliers contributing to high risk and poor consistency


📌 Purpose: To discover hidden operational risks and guide optimization strategies.

3️⃣ DAX Measures & Analytical Modeling

Utilized DAX measures in Power BI to:


Calculate key vendor performance indicators such as:


% Late Orders, % Quantity Mismatch, and % Small Orders


Average Delivery Delay, Avg Lead Time, Avg Spend per Order


Build composite risk scores:


PurchasingHealthScore, Delivery Risk, RejectedRateScore


Identify HighRiskVendors using custom flags and percentiles


Detect unusual behavior and patterns:


Spend_ChangePercent to monitor fluctuations in monthly purchases


Bunching Index and Bunching Alert to identify clustering of orders

📌 Screenshots of calculated DAX logic, sample results, and visual outputs were attached to illustrate methodology.

<img width="259" height="509" alt="image" src="https://github.com/user-attachments/assets/10fa3e42-95ea-4a89-a0d2-b9bf05da06ee" />

<img width="225" height="507" alt="image" src="https://github.com/user-attachments/assets/d17b5ab2-5914-4819-8849-80d98bc5ebdb" />

📌 Purpose: Provide data-driven evidence to support strategic vendor management and operational decisions.

4️⃣ Data Visualization with Power BI


Developed six interactive dashboards with advanced drill-down capabilities to support strategic decision-making:


- Purchase Overview:

Provided an executive summary of purchasing trends across time, vendors, and product categories, enabling quick identification of spending patterns.

- Vendor Effectiveness:

Visualized supplier performance by on-time delivery, quantity mismatch, and rejection rate, helping evaluate consistency and reliability.

- Supply & Delivery Risks:

Highlighted suppliers with high delivery delays, bunching patterns, and delivery risks, using color-coded warnings and time-based trends.

- Purchasing Health:

Built a composite Purchasing Health Score by region and vendor, using normalized metrics like spend efficiency, rejection, and delivery quality.

- Order Optimization:

Identified opportunities to reduce small or fragmented orders, track order frequency, and recommend bundling to increase cost-efficiency.

- Key Findings & Strategic Inputs:

Summarized actionable insights with strategic recommendations based on DAX-driven KPIs, data modeling, and visual storytelling.

✔️ Built dynamic relationships between dimension and fact tables to ensure seamless filtering across dashboards.

📌 Purpose: Deliver clear, actionable insights to drive improvements in purchasing efficiency, vendor collaboration, and risk mitigation.

***

📊 Key Insights & Visualizations
---
🔍 Dashboard Preview


1️⃣ Dashboard 1 Preview

<img width="997" height="503" alt="image" src="https://github.com/user-attachments/assets/0dec63fa-185c-4226-906b-0c5047807021" />

📌 Analysis 1:

Observation:

The total purchase spend is $33.2M across 1.2 million orders, with an average unit price of $27.29.

The top vendor by spend is Superior Bicycles with $2.28M, followed by Bicycle Specialists and Inline Accessories.

The top purchased product is from SUPERSALES INC. with 63K units, significantly ahead of others at 28K units.

Spending over time shows a strong upward trend, peaking at $3.3M, before dropping to $0.4M—indicating possible seasonality or demand spikes.

Recommendation:

Focus on maintaining relationships with top-performing vendors like Superior Bicycles.

Investigate the drop in spending at the end of the period to understand if it's due to inventory saturation, budgeting cycle, or supply disruptions.

Consider negotiating bulk deals with vendors supplying high-volume products such as SUPERSALES INC.

2️⃣ Dashboard 2 Preview

<img width="1001" height="561" alt="image" src="https://github.com/user-attachments/assets/c4bf2c7c-8e16-4131-9759-9e2d73fe7eb6" />

📌 Analysis 2:

Observation:

The total spend remains at $33.2M, but several issues with vendor performance are evident:

The average lead time is 14 days, but there is a significant discrepancy among vendors. For example, G & K Bicycle Corp. has a lead time of 141 days, while many others are only around
30 days.

A 100% late order rate is observed in multiple vendors such as Fitness Association, G & K Bicycle Corp., and Green Lake Bike Company, indicating high delivery risk and reliability concerns.

The highest rejected quantity rates come from Greenwood Athletic Company (5.68%), followed by Proseware, Inc., and SUPERSALES INC.

Spending is still concentrated on top vendors like Superior Bicycles, Bicycle Specialists, and Inline Accessories.


Recommendation:

Reassess vendors with excessive lead times and 100% late delivery rates to evaluate their supply capability and contractual obligations.

Prioritize renegotiation or replacement of vendors with high defect/rejection rates to minimize quality risks and reverse logistics costs.

Establish vendor performance KPIs (lead time, quality, punctuality, and spend) and monitor them periodically to improve supply chain resilience.

3️⃣ Dashboard 3 Preview

<img width="1001" height="562" alt="image" src="https://github.com/user-attachments/assets/4cca9af7-6ff8-4084-9e15-68a20ad53f1a" />

📌 Analysis 3:

Observations:

The Late Order Rate is relatively high at 29.9%, with 12 late deliveries recorded.

The vendors with the most late deliveries are Integrated Sport Products (4 late orders) and Green Lake Bike Company, Jeff’s Sporting Goods (2 each).

The Quantity Mismatch Rate stands at 5.21%, with over 12,599 mismatched items, primarily from International Sport Assoc. (574 items) and Anderson’s Custom Bikes (492 items).

The most frequently stocked-out product is LL Mountain Tire (122 times), followed by various pedal types (Touring, ML, HL).

The product categories with the highest quantity mismatches are Components (3.7K) and Accessories (1.6K) — highlighting critical areas of concern in the supply chain.

Although 99.7% of deliveries are on time, the remaining 0.3% late deliveries may still impact customer satisfaction and service quality if left unaddressed.


Recommendations:
Implement early warning alerts for vendors with a track record of late deliveries, such as Integrated Sport Products and Green Lake Bike Company, to proactively manage delivery timelines.
Reassess supplier performance for those with high mismatch rates and consider applying stricter quality checks before accepting deliveries.
For products with frequent stockouts (e.g., tires and pedals), establish safety stock policies and enhance demand forecasting accuracy.
Include “Delivery Accuracy” and “Quantity Accuracy” as key metrics in the vendor KPI dashboard to monitor supplier performance in real time.


3️⃣ Dashboard 4 Preview

<img width="1000" height="563" alt="image" src="https://github.com/user-attachments/assets/083732d9-a784-40bf-94a2-f32f82c2abad" />

📌 Analysis 4:

Observations:

The overall Purchasing Health Score is relatively strong at 89.87, indicating good performance in procurement operations.

However, High-Risk Vendors account for 89%, and Delivery Risk is at 100%, signaling a serious concern in vendor reliability.

Price Stability is extremely volatile with a value of -152%, implying inconsistent pricing from suppliers.

The Order Rejection Rate is 4%, which is still manageable but should be monitored.

Over 80% of vendors have a low credit rating, and 89.42% of vendors fall into the high-risk category, reinforcing the need for supplier quality improvement.

Lead Time Trend and Total Order Quantity Trend both show a steady decline from August to October, suggesting potential disruptions in supply chain performance.

The Monthly Purchasing Cost has increased significantly from $0M in 2011 to $21M in 2014, indicating rising costs that require budget control.


Recommendations:

Review and evaluate vendor contracts, especially those contributing to high delivery risk and price instability. Focus on supplier negotiation and diversification.

Develop a vendor improvement program targeting low-credit and high-risk suppliers, or consider supplier replacement for persistent underperformance.

Conduct root-cause analysis on price fluctuations to determine whether volatility is due to market changes or vendor inconsistency.

Closely monitor lead time and order quantity trends, and work with operations and forecasting teams to anticipate and address demand issues.

Implement a scorecard-based vendor management system to track improvements over time across quality, reliability, cost, and responsiveness.

📌 Analysis 5:


Observations:
The Bunching Index is 1.50, which falls within the normal distribution, indicating that order placement is moderately spaced throughout the year.

There is a steady decline in monthly orders, dropping from 456 in July to 120 in October, which may point to seasonal purchasing behavior or demand fluctuations.

The Order Frequency over Time trend shows consistent growth, reaching 2.4K orders in 2014, suggesting an overall increase in procurement activity over the years.

100% of orders are categorized as small orders, highlighting a potential issue in purchasing strategy, particularly inefficiencies in batch ordering.

Products like HL Mountain Frame - Silver are repeatedly ordered in low quantities, indicating an opportunity to consolidate orders for efficiency.

The Order Frequency vs Unit Price scatterplot reveals several low-frequency, high-unit-price items, such as Touring-Panniers, Large and Rear Brakes, which could benefit from better planning.


Recommendations:

Consolidate small orders into fewer, larger batch purchases to reduce handling costs and improve supplier negotiations.

Review frequently ordered low-quantity items (e.g., HL Mountain Frame) and implement minimum order quantity (MOQ) policies to optimize supply chain flow.

Investigate declining monthly order trends for potential root causes such as seasonality, internal delays, or stock level planning.

Segment products based on order frequency and cost to define strategic procurement categories: high-cost low-frequency items should be reviewed for potential long-term contracts.

Implement automated reorder thresholds for consistently demanded items to avoid frequent small-volume purchases.
***

🔎 Final Conclusion & Recommendations


<img width="1001" height="563" alt="image" src="https://github.com/user-attachments/assets/2808d739-2e9f-46c3-8aed-b94054e6e24e" />
***


🚨 KEY ISSUES
___
1. High Late Order Ratio (29.9%)

Caused by peak demand periods

Linked to warehouse limitations or operational inefficiencies

2. High Concentration on Risky Vendors (89%)

Risk: Delayed or inefficient deliveries

Recommendation: Renegotiate contracts or seek more reliable suppliers

3. Rising Mismatch in Small Orders (5.2%)

Risk: Higher transportation and shipping costs

Recommendation: Establish a minimum order threshold

💡 Strategic Inputs

A. Rising Costs Due to Frequent Late Deliveries

Use scorecards to analyze cost trends

Recommendation: Compare on-time vs. late delivery costs using a line chart – to be reviewed by the Operations Team

B. Increase in Mismatch Rate Over Time

Monitor mismatch trends against defined benchmarks (e.g., 12%)

Use time-series charts to detect abnormal spikes

C. Small Orders Exceeding Threshold

Redefine the threshold for identifying small orders

Adjust filtering logic to isolate by vendor

D. Risk Rating Scorecard for Vendors

Evaluate vendors by risk level:

Stable → Green

Watchlist → Yellow

High Risk → Red

Base evaluation on credit ratings and delivery performance

E. Benchmark Pricing Control

Establish benchmark prices by product or category

Prioritize renegotiation with vendors whose prices exceed the industry average

🛠️ 90-Day Action Plan

Phase 0–30 Days

Action: Review delivery timelines and identify operational bottlenecks

Owner: Procurement Team

Phase 30–60 Days

Action: Engage with high-risk vendors, review SLAs, and renegotiate terms

Owner: Supplier Management

Phase 60–90 Days

Action: Pilot a consolidated order strategy

Owner: Supply Chain Manager







