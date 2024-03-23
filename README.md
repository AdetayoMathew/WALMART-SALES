# Walmart Sales Data Analysis

## About
This project aims to explore the Walmart Sales data to understand top-performing branches and products, sales trends of different products, and customer behavior. The dataset was obtained from the Kaggle Walmart Sales Forecasting Competition.

## Purposes Of The Project
The major aim of this project is to gain insight into the sales data of Walmart to understand the different factors that affect sales of the different branches.

## About Data
The dataset contains sales transactions from three different branches of Walmart, respectively located in Mandalay, Yangon, and Naypyitaw. It consists of 17 columns and 1000 rows.

| Column Name         | Description                                | Data Type      |
|---------------------|--------------------------------------------|----------------|
| invoice_id          | Invoice of the sales made                  | VARCHAR(30)    |
| branch              | Branch at which sales were made            | VARCHAR(5)     |
| city                | The location of the branch                 | VARCHAR(30)    |
| customer_type       | The type of the customer                   | VARCHAR(30)    |
| gender              | Gender of the customer making purchase     | VARCHAR(10)    |
| product_line        | Product line of the product sold           | VARCHAR(100)   |
| unit_price          | The price of each product                  | DECIMAL(10, 2) |
| quantity            | The amount of the product sold             | INT            |
| VAT                 | The amount of tax on the purchase          | FLOAT(6, 4)    |
| total               | The total cost of the purchase             | DECIMAL(10, 2) |
| date                | The date on which the purchase was made    | DATE           |
| time                | The time at which the purchase was made    | TIMESTAMP      |
| payment_method      | The total amount paid                      | DECIMAL(10, 2) |
| cogs                | Cost Of Goods sold                         | DECIMAL(10, 2) |
| gross_margin_pct    | Gross margin percentage                    | FLOAT(11, 9)   |
| gross_income        | Gross Income                               | DECIMAL(10, 2) |
| rating              | Rating                                     | FLOAT(2, 1)    |

## Analysis List
1. **Product Analysis**: Conduct analysis on the data to understand the different product lines, the product lines performing best, and the product lines that need improvement.
2. **Sales Analysis**: Analyze sales trends of products to measure the effectiveness of sales strategies and identify necessary modifications for increased sales.
3. **Customer Analysis**: Uncover different customer segments, purchase trends, and the profitability of each customer segment.

## Approach Used
- **Data Wrangling**: Inspect data to ensure NULL values and missing values are detected and replaced.
- **Build a Database**: Create tables and insert the data. Select columns with null values and handle them accordingly.
- **Feature Engineering**: Generate new columns from existing ones to provide additional insights into sales data.
- **Exploratory Data Analysis (EDA)**: Analyze data to answer specific questions and address project aims.

## Business Questions To Answer
### Generic Question
- How many unique cities does the data have?
- In which city is each branch?
### Product
- How many unique product lines does the data have?
- What is the most common payment method?
- What is the most selling product line?
- What is the total revenue by month?
- What month had the largest COGS?
- What product line had the largest revenue?
- What is the city with the largest revenue?
- What product line had the largest VAT?
- Fetch each product line and add a column to those product line showing "Good", "Bad". Good if it's greater than average sales.
- Which branch sold more products than the average product sold?
- What is the most common product line by gender?
- What is the average rating of each product line?
### Sales
- Number of sales made in each time of the day per weekday
- Which of the customer types brings the most revenue?
- Which city has the largest tax percent/ VAT (Value Added Tax)?
- Which customer type pays the most in VAT?
### Customer
- How many unique customer types does the data have?
- How many unique payment methods does the data have?
- What is the most common customer type?
- Which customer type buys the most?
- What is the gender of most of the customers?
- What is the gender distribution per branch?
- Which time of the day do customers give most ratings?
- Which time of the day do customers give the most ratings per branch?
- Which day of the week has the best avg ratings?
- Which day of the week has the best average ratings per branch?

## Revenue And Profit Calculations
- $ COGS = unitPrice * quantity $
- $ VAT = 5% * COGS $
- Total (gross_sales) = VAT + COGS
- Gross Profit (grossIncome) = Total (gross_sales) - COGS
- Gross Margin = Gross profit expressed as a percentage of total revenue

Example with the first row in our DB:
Data given:
- Unit Price = 45.79
- Quantity = 7
- COGS = 45.79 * 7 = 320.53
- VAT = 5% * COGS = 5% 320.53 = 16.0265
- Total = VAT + COGS = 16.0265 + 320.53
- Gross Margin Percentage = Gross Income / Total Revenue = 16.0265 / 336.5565 ≈ 0.047619 (approximately 4.7619%)

## Code
For the rest of the code, check the SQL_queries.sql file

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales(
    invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12, 4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12, 4),
    rating FLOAT(2, 1)
);
