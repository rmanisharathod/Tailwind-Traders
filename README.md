Tailwind Traders Sales & Profit Insights

Overview

The Tailwind Traders Power BI Report provides a deep analysis of sales performance, profitability, customer trends, and inventory insights. It incorporates **Python scripting for currency exchange calculations, DAX functions for financial metrics, and visual analytics to track customer behavior, stock levels, and tax distributions. The report standardizes sales and profit figures by converting them into USD, ensuring accurate financial comparisons across regions.


Data Processing Using Python

A Python script is used to create a currency exchange table, converting financial data into multiple currencies for standardized reporting.  

Python Script for Exchange Rate Calculation
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
This exchange rate table ensures consistent financial reporting by converting local revenue values into USD.


DAX Functions for Key Financial Metrics  

1. Sales & Profitability Analysis**  
 - Median Sales:
  ```DAX
  Median Sales = MEDIAN('Sales'[Gross Revenue])
  ```
- Yearly Profit Margin:
  ```DAX
  Yearly Profit Margin = DIVIDE(SUM('Sales'[Gross Revenue]),SUM('Sales'[Net Revenue]),BLANK())
  ```
- Yearly Profit Margin Column:
  ```DAX
  Yearly Profit Margin column = 'Sales'[Gross Revenue]/'Sales'[Net Revenue]
  ```
- Year-To-Date (YTD) Profit:
  ```DAX
  YTD Profit = TOTALYTD([Yearly Profit Margin], 'Calendar'[Date])
  ```


Currency Conversion & USD-Based Reporting

To standardize financial data, a new table (Sales in USD) is created using **DAX functions**, incorporating exchange rates.

 DAX Function for Sales in USD Table**  
  ```DAX
   Sales in USD = ADDCOLUMNS(
    Sales, 
    "Country Name", RELATED(Countries[Country]), 
    "Exchange Rate", RELATED('Exchange Data'[Exchange Rate]), 
    "Exchange Currency", RELATED('Exchange Data'[Exchange Currency]), 
    "Gross Revenue USD", [Gross Revenue] * RELATED('Exchange Data'[Exchange Rate]), 
    "Net Revenue USD", [Net Revenue] * RELATED('Exchange Data'[Exchange Rate]), 
    "Total Tax USD", [Total Tax] * RELATED('Exchange Data'[Exchange Rate]))

```
This ensures financial metrics are consistent across different currencies.


DAX Measures for USD-Based Financial Analysis

- Median Sales (USD)
  ```DAX
  Median Sales USD = MEDIAN('Sales in USD'[Gross Revenue USD])
  ```
- Quarterly Profit (USD)
  ```DAX
  Quarterly Profit USD = CALCULATE([Yearly Profit Margin USD],DATESQTD('Calendar'[Date]))
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

Additional Customer & Inventory Insights

The report goes beyond financial analysis by including **customer preferences, inventory status, and sales performance per representative**.

1. Customer Behavior & Preferences
 - Popular Products: Identifies best-selling products in different regions.  
 - Color Choices in Orders: Analyzes product color preferences among customers.  
 - Customer Ratings: Evaluates satisfaction scores based on product category.  
 - Loyalty Points Distribution: Measures customer retention and engagement.

2. Warehouse & Stock Insights
 - Stock Availability by Category: Displays product inventory levels across different warehouses.  
 - Quantity Sold per Product: Tracks demand trends for different product categories.

3. Tax & Revenue Distribution
 - Sum of Tax per Product: Calculates the total tax collected for different product categories.  
 - Gross Revenue vs. Gross Product Price: Compares revenue generated against the original product cost.

4. Sales Representative Performance
 - Sales by Representative: Tracks individual sales performance and contributions to total revenue.
 - Regional Sales Impact: Identifies which representatives drive the most sales in specific markets.

Conclusion

The Tailwind Traders Power BI Report offers a holistic view of sales, profitability, customer trends, and inventory insights. With Python-based currency standardization and DAX-driven financial calculations, this report empowers data-driven decision-making and ensures consistent financial reporting in multiple currencies.
