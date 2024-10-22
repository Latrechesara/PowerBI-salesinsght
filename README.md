# PowerBI-salesinsght
## Problem statement:
This project provides a comprehensive guide to executing a sales data analysis project, simulating how similar projects are handled in large companies. The case study focuses on a computer hardware business facing challenges in a dynamically changing market. To respond to these challenges, the Sales Director has invested in a Power BI dashboard that delivers real-time sales insights, allowing the company to make informed decisions quickly.

### 1- Data & Data modelling:
The data for this project comes from AtliQ Hardware, a company that supplies computer hardware. The dataset contains sales, customer, product, and market information, providing a comprehensive view of the company’s operations. This real-world data is used to build a Power BI dashboard that offers real-time sales insights, helping the company analyze performance and respond to market challenges.

Data MODEl
Below is the **Star Schema** representation of the data model, created using Power BI. It illustrates the relationships between the **Sales Transactions** fact table and its associated dimension tables(sales customers, sales date,sales market,sales product).
![starschema](https://github.com/user-attachments/assets/760edbf5-2360-4dcb-8237-81cff33b6570)

This star schema design optimizes the data model for analytical queries such as sales performance, product trends, and market segmentation. The model can be easily extended by adding more dimensions or metrics to the fact table.
### 3-Data Analysis using SQL:
1. SQL database dump is in db_dump.sql file above. Download `db_dump.sql` file to your local computer and import it as per instructions:
   SQL queries:

1. Show all customer records

    `SELECT * FROM customers;`

1. Show total number of customers

    `SELECT count(*) FROM customers;`

1. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

1. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
1. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

1. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`

### 4-PowerBI dashboard:

I developed an interactive Power BI dashboard to provide real-time sales insights for a computer hardware business operating in a dynamic market. The dashboard helps decision-makers monitor key performance indicators such as revenue, sales quantity, customer behavior, and market trends, facilitating timely and informed business decisions.
![dashboard](https://github.com/user-attachments/assets/5bdcbb0a-ad6a-4571-bef8-b00dac2ad31e)

** Data Preparation and Cleaning:
To ensure data accuracy and relevance, I performed extensive data cleaning, including the elimination of duplicate and meaningless values. Using formulas like:

** Filtering sales transactions:

Table.SelectRows(sales_transactions, each ([sales_amount] <> -1 and [sales_amount] <> 0))
Currency conversion:

Table.AddColumn(#"Filtered Rows", "norm_sales_amount", each if [currency] = "USD" then [sales_amount]*75 else [sales_amount])
This step ensured that only valid and consistent data was used in the analysis.

** Dashboard Features:
Revenue and Sales Quantity per Market: I added key measures, including:

Revenue:

Revenue = SUM('sales transactions'[sales_amount])
Sales Quantity:

-Sales Qty = SUM('sales transactions'[sales_qty])
These metrics are visualized across different markets, allowing users to track performance in specific geographic regions.

-Year and Time Filtering: The dashboard includes a time filter, enabling users to view sales quantity and revenue for specific years and time periods, providing a dynamic and focused view of the data.

-Revenue Trend Graph: A visual representation of revenue trends over time has been added, helping users understand sales performance changes and growth patterns across different periods.

-Top 5 Customers and Products: To highlight key drivers of sales, the dashboard features a ranking of the top 5 customers and top 5 products, offering insights into which customers and products contribute most to the business.

