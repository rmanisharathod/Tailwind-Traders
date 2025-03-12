Power BI Report: Currency Exchange & Sales Analysis

Overview
This Power BI report provides insights into sales performance across different currencies by integrating an exchange rate table and calculating sales metrics in USD. It includes key calculations, DAX functions, and Python transformations to ensure accurate financial analysis.


Data Transformation Using Python
A Python script was used to create a new exchange rate table that converts sales data into multiple currencies.

```python
import pandas as pd 
from io import StringIO

data = """Exchange ID;ExchangeRate;Exchange Currency
1;1;USD
2;0,75;GBP
3;0,85;EUR
4;3,67;AED
5;1,3;AUD"""
df = pd.read_csv(StringIO(data), sep=';')

# Return the transformed dataframe
df   
```
This table allows conversions between currencies based on predefined exchange rates.

---

DAX Calculations and Measures
The following measures were created to analyze sales and profitability:

Sales Metrics
- Median Sales
  ```DAX
  Median Sales = MEDIAN('Sales'[Gross Revenue])
  ```

- Yearly Profit Margin
  ```DAX
  Yearly Profit Margin = DIVIDE(SUM('Sales'[Gross Revenue]),SUM('Sales'[Net Revenue]),BLANK())
  ```

- Yearly Profit Margin Column
  ```DAX
  Yearly Profit Margin column = 'Sales'[Gross Revenue]/'Sales'[Net Revenue]
  ```

- Year-To-Date (YTD) Profit
  ```DAX
  YTD Profit = TOTALYTD([Yearly Profit Margin], 'Calendar'[Date])
  ```


Currency Conversion in Power BI
A new table, **Sales in USD**, was created using a DAX function to incorporate exchange rates and convert sales figures into USD.

DAX Function for New Table:
```DAX
Sales in USD = ADDCOLUMNS(
    Sales, 
    "Country Name", RELATED(Countries[Country]), 
    "Exchange Rate", RELATED('Exchange Data'[Exchange Rate]), 
    "Exchange Currency", RELATED('Exchange Data'[Exchange Currency]), 
    "Gross Revenue USD", [Gross Revenue] * RELATED('Exchange Data'[Exchange Rate]), 
    "Net Revenue USD", [Net Revenue] * RELATED('Exchange Data'[Exchange Rate]), 
    "Total Tax USD", [Total Tax] * RELATED('Exchange Data'[Exchange Rate])
)
```
This table ensures all sales and tax figures are normalized to USD for consistent financial reporting.

---

Additional DAX Calculations for USD Metrics
For analysis in USD, the following measures were created:

- Median Sales USD
  ```DAX
  Median Sales USD = MEDIAN('Sales in USD'[Gross Revenue USD])
  ```

- Quarterly Profit USD
  ```DAX
  Quarterly Profit USD = CALCULATE([Yearly Profit Margin USD], DATESQTD('Calendar'[Date]))
  ```

- Yearly Profit Margin Column (USD)
  ```DAX
  Yearly Profit Margin column USD = 'Sales in USD'[Gross Revenue USD] / 'Sales in USD'[Net Revenue USD]
  ```

- Yearly Profit Margin (USD)
  ```DAX
  Yearly Profit Margin USD = DIVIDE(SUM('Sales in USD'[Gross Revenue USD]),SUM('Sales in USD'[Net Revenue USD]),BLANK())
  ```

- Year-To-Date (YTD) Profit (USD)
  ```DAX
  YTD Profit USD = TOTALYTD([Yearly Profit Margin USD], 'Calendar'[Date]) 
  ```

Key Insights


1. Sales & Profitability Analysis

- Sales Performance by Date & Country: Displays sales trends over time and identifies top-performing regions.

- Gross Revenue & Net Revenue: Provides an overview of total sales and net earnings across multiple locations.

- Yearly & Quarterly Profit Margins: Analyzes profitability ratios, allowing comparison across different time periods.

Currency-Adjusted Sales: Converts revenue figures to USD for consistent financial analysis.

2. Customer Trends & Product Preferences

- Popular Products & Categories: Identifies the best-selling items across different regions.

- Color Preferences in Orders: Tracks product orders based on color preferences, showing customer buying behavior.

- Customer Ratings by Product Category: Evaluates customer feedback across various product lines.

- Loyalty Points by Country: Analyzes customer retention through the distribution of loyalty points.

3. Warehouse & Inventory Insights

- Stock Levels by Product Category: Displays available inventory for different product categories.

- Quantity Sold Analysis: Tracks the number of units sold per product, highlighting demand trends.

4. Tax & Revenue Breakdown

- Sum of Tax per Product: Provides tax distribution insights across different product types.

- Gross Revenue vs. Gross Product Price: Compares total revenue generated against product costs to assess profitability.

5. Sales Representative Performance

- Sales by Representative: Identifies top-performing sales representatives and their contribution to overall revenue

Conclusion
This Power BI report integrates exchange rate transformations using Python and DAX calculations to provide a comprehensive view of sales performance across multiple currencies offering deep insights into sales, customer behavior, inventory levels, and financial performance. With real-time data visualization and standardized currency reporting, it enables stakeholders to make informed business decisions.
