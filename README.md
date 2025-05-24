# 📈 Tailwind Traders Sales & Profit Insights

![Power BI](https://img.shields.io/badge/Tool-PowerBI-yellow.svg)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Data Source](https://img.shields.io/badge/Data-Exchange%20%7C%20Sales%20%7C%20Customers-lightgrey.svg)

> An end-to-end business intelligence report built with **Power BI**, leveraging **Python** and **DAX** for advanced financial metrics, currency conversion, customer behavior analysis, inventory insights, and sales performance tracking.

---

## 📌 Project Highlights

- 💹 **Power BI dashboards** visualizing key metrics and business KPIs
- 💱 **Currency conversion** from multiple currencies to USD using Python
- 📊 **DAX functions** for advanced calculations like median sales, profit margin, and YTD metrics
- 🧠 **Customer behavior insights** including preferences, ratings, and loyalty
- 🏢 **Inventory and warehouse analysis** to monitor stock and demand trends
- 🧑‍💼 **Sales rep performance tracking** by region and revenue contribution

---

## 🧪 Technologies Used

| Tool         | Purpose                              |
|--------------|--------------------------------------|
| Power BI 📊   | Interactive dashboards & reports     |
| Python 🐍     | Currency conversion scripting        |
| DAX 🧮        | Calculated metrics & measures        |
| Pandas 📈     | Data manipulation for preprocessing  |

---

## 🔁 Currency Conversion with Python

A Python script was used to create a reliable currency exchange reference table for financial standardization.
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
✅ Result: All financial figures are normalized to USD across reports for consistent global comparisons.

---
## 🧾 **DAX Functions for Key Financial Metrics**

📊 **Sales & Profitability Metrics**

* Median Sales
```
Median Sales = MEDIAN('Sales'[Gross Revenue])
```
* Yearly Profit Margin
```
Yearly Profit Margin = DIVIDE(SUM('Sales'[Gross Revenue]), SUM('Sales'[Net Revenue]), BLANK())
```
* Year-To-Date (YTD) Profit
```
YTD Profit = TOTALYTD([Yearly Profit Margin], 'Calendar'[Date])
```
---
## 💵 USD-Based Financial Reporting

To ensure currency-consistent reporting, a new table Sales in USD was created:
```
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
## 💰 USD-Based Metrics

Median Sales (USD)
```
Median Sales USD = MEDIAN('Sales in USD'[Gross Revenue USD])
Quarterly Profit (USD)
```
Quarterly Profit (USD)
```
Quarterly Profit USD = CALCULATE([Yearly Profit Margin USD], DATESQTD('Calendar'[Date]))
```
Year-To-Date (YTD) Profit (USD)
```
YTD Profit USD = TOTALYTD([Yearly Profit Margin USD], 'Calendar'[Date])
```
---

## 🧍 Customer Behavior & Preferences

| Metric                  | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| 🔥 **Popular Products** | Regional best-selling items                             |
| 🎨 **Color Choices**    | Preferences based on product color                      |
| ⭐ **Customer Ratings**  | Satisfaction levels per product category                |
| 🎁 **Loyalty Points**   | Distribution & engagement tracking for repeat customers |

---

## 🏬 Warehouse & Inventory Insights

| Insight                               | Purpose                                    |
| ------------------------------------- | ------------------------------------------ |
| 🗂 **Stock Availability by Category** | Real-time warehouse-level inventory levels |
| 📦 **Quantity Sold per Product**      | Demand trends across product types         |

---

## 💵 Tax & Revenue Distribution

| Metric                                | Description                         |
| ------------------------------------- | ----------------------------------- |
| 🧾 **Tax per Product**                | Total tax collected by product type |
| 💸 **Gross Revenue vs. Product Cost** | Profitability and markup assessment |

---

## 🧑‍💼 Sales Representative Performance

| Metric                         | Purpose                                         |
| ------------------------------ | ----------------------------------------------- |
| 🧍 **Sales by Representative** | Individual revenue contribution tracking        |
| 🌎 **Regional Sales Impact**   | Highlights top-performing reps by market region |

---

## 📊 Insight Charts Overview: Visualizing Key Business Metrics

| 📈 Plot Title                             | 📊 Chart Type     | 🧾 Columns Used                         | 🔍 Purpose                                      |
| ----------------------------------------- | ----------------- | --------------------------------------- | ----------------------------------------------- |
| Orders by Color and Size                  | Stacked Bar Chart | Color, Size, Number of Orders           | Understand customer preferences by color & size |
| Customer Ratings by Category              | Line Chart        | Product Category, Sum of Rating         | Evaluate satisfaction across product categories |
| Loyalty Points vs. Product Stocks         | Clustered Bar     | Product Category, Loyalty Points, Stock | Compare engagement with product availability    |
| Tax Collected per Product                 | Horizontal Bar    | Product Category, Tax Amount            | Analyze tax contribution per category           |
| Sales by Sales Representatives            | Pie Chart         | Sales Rep Name, Sales Count             | Breakdown of sales performance by reps          |
| Gross Revenue vs. Product Cost (Quantity) | Bubble Chart      | Gross Revenue, Gross Product Price      | Visualize profitability by cost and volume      |
| Net Revenue by Product                    | Bar Chart         | Product Name, Net Revenue USD           | Highlight top-earning individual products       |
| Net Revenue by Country                    | Donut Chart       | Country Name, Net Revenue USD           | Compare revenue contributions per region        |
| Yearly Profit Margin Over Time            | Area Chart        | Date, Yearly Profit Margin USD          | Track profitability trends over the year        |
| Gross Revenue USD by Date                 | Line Chart        | Date, Gross Revenue USD                 | View daily revenue flows over time              |

---

## 📸 Sample Visualizations

<table>
  <tr>
    <td><img src="sales_and_profit_overview.PNG" alt="Sales and Profit Overview" width="400"/></td>
    <td><img src="usd_sales_overview.PNG" alt="USD Sales Overview" width="400"/></td>
  </tr>
  <tr>
    <td align="center">Sales and Profit Overview</td>
    <td align="center">USD Sales Overview</td>
  </tr>
  <tr>
    <td colspan="2" align="center"><img src="usd_profit_overview.PNG" alt="USD Profit Overview" width="400"/></td>
  </tr>
  <tr>
    <td colspan="2" align="center">USD Profit Overview</td>
  </tr>
</table>

📊 Each chart brings unique business insights—from customer behavior to sales rep impact and profit trends.

---

## 🧍 Customer Behavior & Preferences

| Metric                  | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| 🔥 **Popular Products** | Most frequently ordered items per region              |
| 🎨 **Color Choices**    | Product preferences across different sizes and colors |
| ⭐ **Customer Ratings**  | Satisfaction distribution across categories           |
| 🎁 **Loyalty Points**   | Track customer engagement and retention efforts       |

---

## 🏬 Warehouse & Inventory Insights

| Insight                  | Purpose                                    |
| ------------------------ | ------------------------------------------ |
| 🗂 **Stock by Category** | Displays inventory health by category      |
| 📦 **Quantity Sold**     | Measures product demand and stock movement |

---

## 💵 Tax & Revenue Distribution

| Metric                        | Description                              |
| ----------------------------- | ---------------------------------------- |
| 🧾 **Tax per Product**        | Tax contribution by product category     |
| 💸 **Gross Revenue vs. Cost** | Profitability analysis across categories |

---

## 🧑‍💼 Sales Representative Performance

| Metric                         | Purpose                                            |
| ------------------------------ | -------------------------------------------------- |
| 🧍 **Sales by Representative** | Tracks individual contributions to overall revenue |
| 🌍 **Regional Sales Impact**   | Measures rep performance by territory              |

---

## 🧭 File Structure

```bash
tailwind-traders-report/
├── Python/
│   └── currency_conversion.py    # Currency exchange rate script
├── PowerBI/
│   └── Tailwind_Report.pbix      # Power BI report file
├── DAX_Measures/
│   └── dax_metrics.txt           # DAX formulas and measures
└── README.md                     # Project documentation
```

---

## 🚀 Getting Started

1. **Clone the Repository**
```bash
git clone https://github.com/your-username/tailwind-traders-report.git
cd tailwind-traders-report
```

2. **Open Power BI Report**

* Open Tailwind_Report.pbix in Power BI Desktop.

3. **Run Currency Conversion Script (Optional)**

```bash
cd Python
python currency_conversion.py
```
---



---

## 📜 License
This project is licensed under the MIT License.
Use, modify, and share with attribution.

---

## 🙌 Acknowledgments

Gratitude to:
* Tailwind Traders Team for the sample data and inspiration
* Developers of Power BI, pandas, and DAX for enabling powerful analytics
* The broader data community for sharing open-source BI resources
---

## 📫 Contact

For feedback, ideas, or collaboration: 
📧 r.manisharathod6@gmail.com
