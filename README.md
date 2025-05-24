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
