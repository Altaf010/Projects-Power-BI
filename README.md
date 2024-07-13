Sales Data Analysis Report

**Introduction**
This report provides a comprehensive analysis of the sales data using SQL queries and Power BI transformations. 
The analysis includes customer records, transactions specific to the Chennai market, and revenue calculations for the year 2020. 
Additionally, a formula to create a normalized amount column in Power BI is discussed.

Customer Records
SELECT * FROM customers;
This query calculates the total number of customers in the database.

Transactions Analysis
SELECT * FROM transactions where market_code='Mark001';
This query retrieves all transactions that took place in the Chennai market, identified by the market code 'Mark001'.

Distinct Product Codes Sold in Chennai
SELECT distinct product_code FROM transactions where market_code='Mark001';
This query lists all distinct product codes that were sold in the Chennai market.

Transactions in US Dollars
SELECT * from transactions where currency="USD";
This query retrieves all transactions where the currency is US dollars.

Revenue Analysis
SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
This query retrieves all transactions from the year 2020 by joining the transactions table with the date table.

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 
and (transactions.currency="INR\r" or transactions.currency="USD\r");
This query calculates the total revenue for the year 2020, considering transactions in both INR and USD currencies.

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 
and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");
This query calculates the total revenue for the Chennai market in the year 2020.

Power BI Data Transformation
To create a norm_amount column in Power BI that normalizes the sales amount based on the currency, use the following formula:
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
This formula adds a new column norm_amount to the table, where the sales amount is multiplied by 75 if the currency is USD. Otherwise, it retains the original sales amount.

Conclusion
This report provides detailed insights into customer records, market-specific transactions, 
and revenue calculations for the year 2020. The SQL queries and Power BI transformations used in this analysis can be further customized to extract more specific insights based on business requirements. 
By utilizing these techniques, businesses can gain a deeper understanding of their sales performance and make informed decisions to drive growth.

