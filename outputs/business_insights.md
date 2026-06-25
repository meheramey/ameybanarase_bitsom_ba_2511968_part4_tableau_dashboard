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
  