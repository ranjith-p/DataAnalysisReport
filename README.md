## Sales Insights Data Analysis Project

The data used in this project is of AtliQ Hardware 

The data is in the form of SQL database. SQL database dump is in `db_dump.sql` file 

First the data is loaded into MySQL database

### There are 5 tables:
1. Customers

2. Date

3. Transactions

4. Markets

5. Products

## Data Analysis Using SQL
1. Show all customer records

`SELECT * FROM customers;`

2. Show total number of customers

`SELECT count(*) FROM customers;`

3. Show transactions for Chennai market (market code for chennai is Mark001)

`SELECT * FROM transactions where market_code='Mark001';`

4. Show distrinct product codes that were sold in chennai

`SELECT distinct product_code FROM transactions where market_code='Mark001';`

5. Show transactions where currency is US dollars

`SELECT * from transactions where currency="USD"`

6. Show transactions in 2020 join by date table

`SELECT t.*, date.* FROM transactions t INNER JOIN date ON t.order_date=date.date where date.year=2020;`

7. Show total revenue in year 2020,

`SELECT SUM(t.sales_amount) FROM transactions t INNER JOIN date ON t.order_date=date.date where date.year=2020 and t.currency="INR\r" or t.currency="USD\r";`

8. Show total revenue in year 2020, January Month,

`SELECT SUM(t.sales_amount) FROM transactions t INNER JOIN date ON t.order_date=date.date where date.year=2020 and date.month_name="January" and (t.currency="INR\r" or t.currency="USD\r");`

9. Show total revenue in year 2020 in Chennai

`SELECT SUM(t.sales_amount) FROM transactions t INNER JOIN date ON t.order_date=date.date where date.year=2020 and t.market_code="Mark001";`


## Import the SQL database into Power BI

### Added a new column 'norm_sales_amount' converting all USD in INR

` Table.AddColumn(sales_transactions, "norm_sales_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount]*75 else [sales_amount])`

### Filtering
` Table.SelectRows(#"Added Conditional Column", each ([sales_amount] <> -1 and [sales_amount] <> 0))`
` Table.SelectRows(sales_markets, each ([zone] <> ""))`

### Generating report 
The generated report file is `Sales_report.pbix`

![alt text](https://github.com/ranjith-p/testing03/blob/master/Report.JPG?raw=true)
