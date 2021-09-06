# Atliq-Hardware-sales-data-analysis

## 📕  Table Of Contents
* 1.📋 PROBLEM STATEMENT 
* 2.🕵 Data discovery/data Cleansing
* 3.🗄 Data Modeling/data Mashup
* 4.📊 Data Visualization

## PROBLEM STATEMENT
AtliQ hardware is a company in India which supplies computer hardware and peripheral devices across India only. The have many stores across India. The head office of the company is situated in Delhi.
The sales manager of the company is facing issues in tracking sales in dynamically growing market.In order to know the performance of company he has different regional managers
from north south and central of India .

#### The problem is that the sales manager is not satisfied with the performance shared by each regional manager as they are sugar coating the facts. Even after knowing that the sales are declining, he cannot do anything because he does not have the clear picture of the sales.So In order to get real insights he is more interested in a Dashboard which gives simple, understandable and digestive insight of the business.He wants to know the weakest area that the company needs to focus to increase the sales and improvise the declination.

All he wants is a simple data visualization tool which he can access on daily basis.

## Data discovery/data cleansing

#### How will the company work —
There is a team of software engineers (falcons) which owns sales management system. The records of this system are stored in MySQL database.
The team of Data Analyst (Data masters) reaches out to the software engineers to get an access to data base which they can use to create the dashboard in PowerBI.

#### In this same manner We are going to fetch the data from the database and then we are going to transform and load the data in the PowerBI to build the dashboard.

* Import the data in MySQL workbench 
<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Data%20import%20in%20MYSQL.png?raw=true" width=50% height=50%>

* Simple analysis of data by looking into different tables and reflecting garbage values in MYSQL-

### Data cleansing -Perfromed ETL in Power Query Editor 

* The table market contains data for international market and AtliQ do not sell in international market so that's a garbage data.Removed them while transforming data.

* Sales amount has some values in USD that we have converted into INR by using current conversion rate bu using DAX.

## Primary analysis of data base by running different SQL statements

1. Show all customer records

    `SELECT * FROM customers;`

2. Show total number of customers

    `SELECT count(*) FROM customers;`

3. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

4. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

5. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

6. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

7. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
8. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

9. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`











