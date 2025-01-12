# Sales Insights Data Analysis Project

This project involves analyzing a sales dataset using SQL and Power BI to derive meaningful insights. The dataset contains customer records, transactions, and revenue information, categorized by markets, products, and timeframes. 

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset Information](#dataset-information)
3. [Setup Instructions](#setup-instructions)
4. [Data Analysis Using SQL](#data-analysis-using-sql)
5. [Data Visualization Using Power BI](#data-visualization-using-power-bi)
6. [Conclusion](#conclusion)
7. [Resources](#resources)
8. [License](#license)

---

## Project Overview
The **Sales Insights Data Analysis Project** uses a structured dataset to answer various business queries and create compelling visualizations. It focuses on:
- Customer transactions and revenue analysis.
- Exploring patterns across different markets.
- Revenue trends over time.

![Sales Dashboard](https://github.com/Gul-Fatima/Sales-Analysis/blob/main/BI%20Dashboard.PNG)

### **Insights from Data Analysis**

- **Delhi drives the highest revenue (520M)**, suggesting it as the top priority for resource allocation and market campaigns.
- **Low-performing markets** like Bhubaneswar and Lucknow need strategic focus to unlock potential or could be deprioritized.
- A small percentage of customers, such as **Electricalsara Stores**, contribute significantly to revenue, highlighting opportunities for loyalty programs and targeted upselling.
- Seasonal trends show **revenue spikes in January**, indicating high sales months for focused marketing.
- Consolidation of revenue data (INR and USD) is crucial for better decision-making and consistent reporting.

**Key Actions:**
- Prioritize top markets for campaigns and allocate resources to Delhi, Mumbai, and Ahmedabad.
- Address pain points in low-performing markets or reallocate efforts.
- Leverage customer trends to build loyalty programs and cross-selling strategies.

---

Technologies used:
- SQL for querying and analyzing data.
- Power BI for visualization.

---

## Dataset Information
The dataset includes the following tables:
- **Customers:** Contains customer details.
- **Transactions:** Includes sales transactions with market codes, product codes, and sales amounts.
- **Date:** Provides details of transaction dates (year, month, day).
- **Markets** Provides geographical information.
- **Products** Provides information about product category.

**Data Source:** The dataset was obtained as part of a tutorial by [codebasics](https://www.youtube.com/watch?v=hhZ62IlTxYs&list=PLeo1K3hjS3utcb9nKtanhcn8jd2E0Hp9b&index=2) and is included in the project as `db_dump.sql`.

---

## Setup Instructions

### Step 1: Install MySQL
Follow [this tutorial video](https://www.youtube.com/watch?v=WuBcTJnIuzo) to install MySQL on your local computer.

### Step 2: Import the Database
1. Download the `db_dump.sql` file from this repository.
2. Import the file into MySQL:
   ```bash
   mysql -u username -p database_name < db_dump.sql
   ```

---

## Data Analysis Using SQL
Here are the SQL queries used for analysis:

1. **Show all customer records:**
   ```sql
   SELECT * FROM customers;
   ```

2. **Show total number of customers:**
   ```sql
   SELECT count(*) FROM customers;
   ```

3. **Show transactions for Chennai market (Market Code: Mark001):**
   ```sql
   SELECT * FROM transactions WHERE market_code='Mark001';
   ```

4. **Show distinct product codes sold in Chennai:**
   ```sql
   SELECT DISTINCT product_code FROM transactions WHERE market_code='Mark001';
   ```

5. **Show transactions where currency is US dollars:**
   ```sql
   SELECT * FROM transactions WHERE currency="USD";
   ```

6. **Show transactions in 2020 (joined with date table):**
   ```sql
   SELECT transactions.*, date.* 
   FROM transactions 
   INNER JOIN date ON transactions.order_date=date.date 
   WHERE date.year=2020;
   ```

7. **Show total revenue in 2020:**
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date=date.date 
   WHERE date.year=2020 AND (transactions.currency="INR\r" OR transactions.currency="USD\r");
   ```

8. **Show total revenue in January 2020:**
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date=date.date 
   WHERE date.year=2020 AND date.month_name="January" AND (transactions.currency="INR\r" OR transactions.currency="USD\r");
   ```

9. **Show total revenue in Chennai in 2020:**
   ```sql
   SELECT SUM(transactions.sales_amount) 
   FROM transactions 
   INNER JOIN date ON transactions.order_date=date.date 
   WHERE date.year=2020 AND transactions.market_code="Mark001";
   ```

---

## Data Visualization Using Power BI
### Key Steps in Power BI
1. **Normalized Sales Amount:**
   Created a new column `norm_amount` to convert USD sales amounts to INR.
   ```powerquery
   = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
   ```

2. **Insights Visualized:**
   - **Revenue by Market:** Bar charts showing revenue by city.
   - **Sales Quantity by Market:** Bar charts displaying sales quantity per market.
   - **Revenue Trends:** Line charts highlighting revenue trends by year, quarter, month, and day.
   - **Top Customers:** Bar charts featuring the top customers by revenue.

---

## Conclusion
This project demonstrates how to leverage SQL and Power BI for sales data analysis. Key findings include:
- Chennai and Delhi contributed significantly to overall revenue.
- Sales quantities and revenue patterns varied across different markets.
- Clear revenue trends were observed over time, which can aid in forecasting and decision-making.

The visualizations and queries provide actionable insights that can help businesses optimize their sales strategy and customer targeting.

---

## Resources
- [MySQL Installation Tutorial](https://www.youtube.com/watch?v=WuBcTJnIuzo)
- Power BI Dashboard Design Guide: [Power BI Documentation](https://docs.microsoft.com/en-us/power-bi/)

---

## License
This project follows the MIT License. Refer to the `LICENSE` file for details.
```

