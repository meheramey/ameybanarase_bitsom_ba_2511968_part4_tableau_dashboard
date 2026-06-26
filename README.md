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
The `tableau/executive_dashboard.twbx` is a fully standalone packaged workbook developed using Tableau. It contains comprehensive data source schemas, pre-calculated metadata layers, and custom visual worksheets compiled into a centralized executive-ready dashboard interface.

---

## 4. Calculated Fields Created
To support advanced visual mapping and business logic, the following calculated fields were constructed natively within the workbook:

| Field | Formula | Purpose |
|-------|---------|---------|
| Profitable Order Flag | `IF [Profit] > 0 THEN "Profitable" ELSE "Loss" END` | Flags loss-making orders |
| Shipping Delay Bucket | DATEDIFF based categorization | Groups orders into Same Day, 2-3 Days, 4-7 Days, 7+ Days |
| Profit Margin | `SUM([Profit]) / SUM([Sales])` | Tracks profit margin % |
| Cost | `SUM([Sales]) - SUM([Profit])` | Total cost incurred |
| Average Order Value | `SUM([Sales]) / COUNTD([Order Id])` | Avg spend per order |
| Return Rate | `SUM(IF [Return Flag]="Yes" THEN 1 ELSE 0 END) / COUNT([Order Id])` | % of returned orders |
| Discount Impact | `SUM([Sales]) * SUM([Discount])` | Revenue lost due to discounts |

---

## 5. Dashboard Components
The interface integrates 5 complementary operational views aligned via a strict grid system:

- **Sales Trend (Line Chart):** Tracks cyclical monthly revenue streams against net profit baselines.
- **Regional Performance (Bar Chart):** Highlights sales and profit performance across regions.
- **Category Profitability (Horizontal Bar Chart):** Compares sub-category margins, exposing high-performing and loss-making lines.
- **Discount Impact (Scatter Plot):** Correlates the exact threshold where discounts actively destroy profit margins.
- **Shipping Delay Bucket (Bar Chart):** Quantifies distribution volume patterns inside sluggish fulfillment cycles.

---

## 6. Filters and Interactions Used
- **Global Filters:** Top-level dropdown filters (Region, Category, Customer Segment) use "All Using This Data Source" dependency. Slicing any single filter updates all charts instantly.
- **Cross-Filtering Tooltips:** Hovering over any data point dynamically reveals contextual tooltips displaying secondary financial health layers.

---

## 7. Key Business Insights
1. **Seasonal Sales:** Sharp revenue peaks occur in Q4 of consecutive fiscal years, followed by deep seasonal drops in Q1.
2. **Geographic Concentration:** Revenue is heavily locked within primary hubs, leaving alternative regional belts under-penetrated.
3. **Sub-Category Margin Erosion:** Technology segment acts as the main profit engine, while Tables sub-category under Furniture operates as a severe loss-leader.
4. **Discount Thresholds:** Margins remain viable under low discounts but degrade sharply into losses once discount rates exceed 20-25%.

---

## 8. Dashboard Story Summary
The overarching narrative connects macro achievements ($33.3M Sales / $3.3M Profit) to operational bottlenecks. It guides leadership from top-line success down to underlying vulnerabilities — exposing how unguided discounts and sluggish supply chain (4-7 Days delivery bucket) undermine our lucrative technology product lines. The story outlines hard guardrails (a 15% discount cap) to stabilize margins.

---

## 9. Assumptions and Limitations
- **Historical Uniformity:** Assumes historical sales trend patterns will carry forward consistently into future forecasting cycles.
- **Customer-Level Blindspot:** Data aggregates macro performance but cannot track individual customer churn rates or sentiment profiles.
- **Static Context:** Lacks external market benchmarking data, competitor tracking, or currency fluctuation matrices.

---

## 10. Screenshots Included

| File | Description |
|------|-------------|
| `screenshots/full_dashboard.png` | Complete operational dashboard layout |
| `screenshots/sales_trend_view.png` | Close-up of sales trend line chart |
| `screenshots/regional_performance_view.png` | Regional performance bar chart |
| `screenshots/category_profitability_view.png` | Sub-category sorted bar chart |
| `screenshots/filter_interaction_view.png` | Proof of dynamic global filter functionality |
