# Retail Operations: Business Insights & Technical Calculations

## 🛠️ Task 2: Tableau Calculated Fields Documentation

To drive deep strategic analysis and cross-functional performance tracking, the following five custom calculated fields were engineered within Tableau Desktop:

1. **Profit Margin**
   * **Formula:** `[Profit] / [Sales]`
   * **Business Logic:** Measures net profitability efficiency per unit of currency generated. It isolates structural financial leaks by identifying regions or products that generate high sales volume but low net returns.

2. **Cost**
   * **Formula:** `[Sales] - [Profit]`
   * **Business Logic:** Calculates the absolute financial expenditure incurred for product production and baseline fulfillment logistics, providing visibility into supply chain efficiency.

3. **Average Order Value (AOV)**
   * **Formula:** `SUM([Sales]) / COUNTD([Order ID])`
   * **Business Logic:** Tracks the average transactional basket size of customers. Essential for evaluating customer purchasing behavior and checking the success of cross-selling strategies.

4. **Return Rate**
   * **Formula:** `COUNTD(IF [Returned] = "Yes" THEN [Order ID] END) / COUNTD([Order ID])`
   * **Business Logic:** Quantifies product return frequencies against total unique orders. Serves as an operational guardrail metric to track quality control issues and post-purchase friction.

5. **Shipping Delay Bucket**
   * **Formula:**
     ```tableau
     IF [Delivery Days] <= 2 THEN "0-2 Days (Fast)"
     ELSEIF [Delivery Days] <= 5 THEN "3-5 Days (Standard)"
     ELSE "6+ Days (Delayed)"
     END
     ```
   * **Business Logic:** Segregates continuous operational fulfillment days into three strategic business buckets to immediately catch SLA breaches and courier distribution bottlenecks.

---