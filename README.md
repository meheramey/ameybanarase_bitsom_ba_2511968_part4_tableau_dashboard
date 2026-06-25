# Part 4: Tableau Executive Dashboard & Data Storytelling

## 📊 Task 1: Data Connection & Inspection Report

### 1. Data Source Connection
The enterprise dataset `dashboard_sales_data.xlsx` has been successfully connected as an active data extract within Tableau Desktop. The data schema was audited to ensure accurate field type assignment before creating visual layers.

### 2. Field Inspection & Data Type Mapping

During the initial data inspection, the following critical dimensions and measures were validated:

* **Date Fields (Temporal):** * `Order Date` and `Ship Date` -> Correctly detected as **Date** data types. These will drive our continuous timeline trends and seasonality analysis.
* **Geographic Fields (Spatial):** * `Country`, `Region`, `State`, and `City` -> Automatically geocoded by Tableau as **Geographic Roles**. These fields will populate our interactive geographic maps to trace spatial performance.
* **Categorical Fields (Dimensions):** * `Category`, `Sub-Category`, `Segment`, and `Ship Mode` -> Mapped as **Text/String** dimensions. These will serve as primary granular slicing attributes across horizontal bar charts and matrices.
* **Numerical Measures (Continuous):** * `Sales`, `Profit`, `Quantity`, and `Discount` -> Evaluated as **Decimal/Whole Numbers** and loaded as continuous measures. These drive our financial aggregations, scatter plots, and mathematical metrics.
* **Binary/Flag Fields:** * `Returned` -> Mapped as a **String/Boolean** flag (`Yes` or null/blank) to calculate structural return frequencies.

---

### 💡 Core Analytical Assumptions & Data Rules

To establish a baseline for our dashboard metrics and calculated expressions, the following structural assumptions have been documented:

1. **Return Status Consolidation:** All transaction records where the `Returned` column is blank or null are strictly assumed to represent **Successful Deliveries (Not Returned)**. 
2. **Fulfillment Timeline:** The dynamic delivery timeframe is calculated as the continuous calendar days elapsed between `Order Date` and `Ship Date`. This assumes standard continuous operation without taking localized regional shipping or warehouse holidays into consideration.
3. **Discount Allocation:** The `Discount` field is treated as a continuous proportion applied uniformly at the transaction line-item level, representing promotional price drops affecting final gross revenue.
4. **Direct Profit Representation:** The `Profit` measure is assumed to reflect direct product margins post-manufacturing and logistics costs, without taking corporate-level operational overheads (like corporate tax or marketing CAC) into account.
# Retail Operations: Business Insights & Technical Calculations

## 🛠️ Task 2: Tableau Calculated Fields Documentation

To drive deep strategic analysis and cross-functional performance tracking, the following seven custom calculated fields were engineered within Tableau Desktop:

---

### 1. Average order value
* **Formula / Logic:** `SUM([Sales]) / COUNTD([Order Id])`
* **Data Type:** Continuous Measure (Currency)
* **Business Purpose:** Tracks the average transactional basket size of customers to evaluate purchasing behavior.

### 2. Cost
* **Formula / Logic:** `[Sales] - [Profit]`
* **Data Type:** Continuous Measure (Currency)
* **Business Purpose:** Calculates the absolute financial expenditure incurred for product production and baseline fulfillment logistics.

### 3. Discount Impact
* **Formula / Logic:** `SUM([Sales]) * SUM([Discount])`
* **Data Type:** Continuous Measure (Currency/Value)
* **Business Purpose:** Calculates the gross financial scale of promotions by compounding total sales volume against the total discount depth.

### 4. Profit Margin
* **Formula / Logic:** `[Profit] / [Sales]`
* **Data Type:** Continuous Measure (Formatted as Percentage `%`)
* **Business Purpose:** Measures net profitability efficiency per unit of currency generated to isolate structural financial leaks.

### 5. Profitable Order Flag
* **Formula / Logic:** 
```tableau
IF [Profit] > 0 THEN "Profitable" ELSE "Loss" END
