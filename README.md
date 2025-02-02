# Atliq-Hardware-sales-data-analysis

## 📕  Table Of Contents
* 1.📋 PROBLEM STATEMENT 
* 2.🕵 Data discovery/data Cleansing
* 3.🗄 Data Modeling/data Mashup
* 4.📊 Data Visualization


## INTRODUCTION
Atliq hardware is a company in India which supplies computer hardware and peripheral devices across India only. They have many stores across India. The head office of the company is situated in Delhi.


## PROBLEM STATEMENT
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


### Primary analysis of data base by running different SQL statements

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

`select * from sales.transactions 
join sales.date
on sales.transactions.order_date=sales.date.date
where sales.date.year=2020;`

7. Show total revenue in year 2020,

    `select sum(sales_amount) as total_revenue
    from sales.transactions
    join sales.date
    on sales.transactions.order_date=sales.date.date
    where sales.date.year=2020;`
	
8. Show total revenue in year 2020, January Month,

    `select sum(sales_amount) as total_revenue_january
    from sales.transactions
    join sales.date
on sales.transactions.order_date=sales.date.date
where sales.date.year=2020 and sales.date.month_name='January';`

9. Show total revenue in year 2020 in Chennai

    `select sum(sales_amount) as total_revenue_Chennai_2020
from sales.transactions
join sales.date
on sales.transactions.order_date=sales.date.date
where market_code='Mark001'
and sales.date.year=2020;`


### Get data in power BI from MYSQL database- Provide your server name and database 


<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Provide%20database%20&%20server%20name.PNG?raw=true" width=50% height=50%>

### Load data in power BI

<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Load%20database%20in%20power%20BI.PNG?raw=true" width=50% height=50%>


## Data Cleansing - Perfromed ETL in Power Query Editor 

* The table market contains data for international market and AtliQ do not sell in international market so that's a garbage data.Removed them while transforming data.

* In sales Transactions table - Sales amount have some values in USD that we have converted into INR by using current conversion rate using DAX created new column 'norm_sales_amount.

**Formula**

norm_sales_amount = Table.AddColumn(sales_transactions, "Norm_sales_amount", each if [currency] = "USD" then [sales_amount]*73 else [sales_amount])

<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Norm_sales_amount%20column.PNG?raw=true" width=50% height=50%>

## Data Modeling

Created Entity-Relationship between tables, the model eventually forms star schema

<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Data%20Modeling.PNG?raw=true" width=50% height=50%>

## Data Visualization/Dashboard

simple visual display of the most important information that decision makers need to help them achieve objectives.

* Key Insights
* Profit Analysis
* Performance insights

### Key Insights -
To increase the sales growth , Sales director need to look into these areas
* Revenue by markets
* Sales Qty by markets
* Revenue Trend
* Top Customer by Revenue
* Top 5 Products by Revenue
* Revenue by Zone(can also be filtered out)
* Sales Quantity by Zone (can also be filtered out)

<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/Key%20Insights.PNG?raw=true" width=50% height =50%>


### Profit Analysis
* Revenue Contribution by market
* Profit margin % by market
* Total profit margin contribution by market in %
* Table- Shows top to bottom customers by Total profit margin contribution in %


<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Profit%20Analysis.PNG?raw=true" width=50% height=50%>


### Performance insights
* Profit margin % by Zone ( Created Dynamic Red Alert in the dashboard whenever performance of a certain zone/zones falls below certain mark)
As chart shows negative or low profit margin %(below 2%) for few zones alterted red mark which indicates these are concerned area.
* Revenue Trend - Shows comparision of revenue from previous year to current year (2020) where line chart indicating profit margin trend.
* Table- Shows Top to bottom customer by Profit margin %.


<img src="https://github.com/sweety21-coder/Atliq-Hardware-sales-data-analysis/blob/main/IMG/Performance%20insights.PNG?raw=true" width=50% height=50%>





