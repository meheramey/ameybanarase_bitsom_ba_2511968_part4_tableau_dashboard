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
---

## 3. Tableau Workbook Description
The `tableau/executive_dashboard.twbx` is a fully standalone, packaged workbook developed using Tableau. It contains comprehensive data source schemas, pre-calculated metadata layers, and custom visual worksheets seamlessly compiled into a centralized, executive-ready dashboard interface.

---

## 4. Calculated Fields Created
To support advanced visual mapping and business logic, the following calculated fields were constructed natively within the workbook:
* **`Profitable Order Flag`**
  ```tableau
  IF [Profit] > 0 THEN "Profitable" ELSE "Loss" END
Shipping Delay Bucket (Differentiates operational turnaround tracking into discrete intervals like Same Day, 2–3 Days, 4–7 Days).

Profit Margin % (SUM([Profit]) / SUM([Sales]) to track margins).
## 5. Dashboard Components
The interface integrates 5 complementary operational views aligned via a strict grid system:

Sales Trend (Dual-Axis Line Chart): Tracks cyclical monthly revenue streams against net profit baselines.

Regional Performance (Geographic Filled Map): Highlights spatial concentration and market share density across states.

Category Profitability (Sorted Horizontal Bar Chart): Compares granular sub-category margins, exposing high-performing and loss-making lines.

Discount Impact (Scatter Plot): Correlates the exact statistical threshold where discounts actively destroy average profit margins.

Shipping Delay Bucket (Vertical Column Chart): Quantifies distribution volume patterns trapped inside sluggish fulfillment cycles.

## 6. Filters and Interactions Used
Global Interactivity: Top-level dropdown filters (Region, Category, Customer Segment) use the "All Using This Data Source" dependency. Slicing any single filter updates all 5 charts instantly.

Cross-Filtering Tooltips: Hovering over any localized data point or geographic state dynamically reveals contextual tooltips displaying secondary financial health layers.

## 7. Key Business Insights
Seasonal Sales timeline: Sharp, predictable revenue peaks occur in the latter half of consecutive fiscal years, followed by deep seasonal drops in Q1.

Geographic Centralization: Revenue is heavily locked within primary hubs like Madhya Pradesh, Maharashtra, and Uttar Pradesh, leaving alternative regional belts under-penetrated.

Sub-Category Margin Erosion: The Technology segment acts as the main profit engine, while the Tables sub-category under Furniture operates as a severe structural loss-leader.

Discount Thresholds: Transactional margins remain viable under low discounts but degrade sharply into severe losses once discount rates exceed the 20% to 25% window.

## 8. Dashboard Story Summary
The overarching narrative connects our macro achievements ($33.3M Sales / $3.3M Profit) to operational bottlenecks. It guides leadership from top-line success down to underlying vulnerabilities—exposing how unguided retail discounts and a sluggish supply chain (4-7 Days delivery bucket) undermine our highly lucrative technology product lines. The story outlines hard guardrails (a 15% discount cap) to stabilize our margins.

## 9. Assumptions and Limitations
Historical Uniformity: Assumes historical sales trend patterns and customer behaviors will carry forward consistently into future forecasting cycles.

Customer-Level Blindspot: The data aggregates macro performance effectively but cannot track individual customer churn rates, sentiment profiles, or granular B2B contract lifecycles.

Static Context: Lacks external market benchmarking data, localized competitor tracking, or currency fluctuation matrices.

## 10. Screenshots Included
The required visual evidence is stored inside the repository for rapid review:

screenshots/full_dashboard.png - Complete operational dashboard layout.

screenshots/sales_trend_view.png - Close-up of dual-axis timeline chart.

screenshots/regional_performance_view.png - Geographic distribution profile map.

screenshots/category_profitability_view.png - Sub-category sorted bar chart matrix.

screenshots/filter_interaction_view.png - Validated proof of dynamic global filter functionality.
