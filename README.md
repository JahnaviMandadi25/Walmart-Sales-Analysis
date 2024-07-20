# Walmart Sales Data Analysis

## About

This project aims to explore Walmart Sales data to identify the top-performing branches and products, understand sales trends, and analyze customer behavior. The goal is to develop strategies to improve and optimize sales. The dataset was sourced from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

"In this recruiting competition, job-seekers are provided with historical sales data for 45 Walmart stores located in different regions. Each store contains many departments, and participants must project the sales for each department in each store. To add to the challenge, selected holiday markdown events are included in the dataset. These markdowns are known to affect sales, but it is challenging to predict which departments are affected and the extent of the impact." [source](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

This project was completed under the guidance of the Code with Prince YouTube channel.

## Project Objectives

The primary objective of this project is to gain insights into Walmart's sales data to understand the various factors that influence sales across different branches.

## Data Overview

The dataset was obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting). It contains sales transactions from three different Walmart branches, located in Mandalay, Yangon, and Naypyitaw. The data includes 17 columns and 1000 rows:

| Column                  | Description                             | Data Type      |
| :---------------------- | :-------------------------------------- | :------------- |
| invoice_id              | Invoice of the sales made               | VARCHAR(30)    |
| branch                  | Branch at which sales were made         | VARCHAR(5)     |
| city                    | The location of the branch              | VARCHAR(30)    |
| customer_type           | The type of the customer                | VARCHAR(30)    |
| gender                  | Gender of the customer                  | VARCHAR(30)    |
| product_line            | Product category                        | VARCHAR(100)   |
| unit_price              | Price per unit of the product           | DECIMAL(10,2)  |
| quantity                | Quantity sold                           | INT            |
| tax_pct                 | Tax percentage                          | FLOAT(6,4)     |
| total                   | Total amount after tax                  | DECIMAL(12,4)  |
| date                    | Date of the transaction                 | DATETIME       |
| time                    | Time of the transaction                 | TIME           |
| payment                 | Payment method                          | VARCHAR(15)    |
| cogs                    | Cost of goods sold                      | DECIMAL(10,2)  |
| gross_margin_pct        | Gross margin percentage                 | FLOAT(11,9)    |
| gross_income            | Gross income                            | DECIMAL(12,4)  |
| rating                  | Customer rating                         | FLOAT(2,1)     |

## Key Questions

1. What are the top 5 product lines based on sales volume?
2. What is the sales performance of each branch?
3. What are the sales trends over different months?
4. How does customer behavior vary by branch?
5. What are the peak sales hours in each branch?
6. How does the average rating differ by branch and time of day?
7. Which day of the week has the highest average ratings?
8. How can sales strategies be optimized based on these insights?

## Revenue and Profit Calculations

\[ \text{COGS} = \text{unit\_price} \times \text{quantity} \]

\[ \text{VAT} = 5\% \times \text{COGS} \]

VAT is added to the COGS to determine the amount billed to the customer.

\[ \text{total\_gross\_sales} = \text{VAT} + \text{COGS} \]

\[ \text{gross\_profit} = \text{total\_gross\_sales} - \text{COGS} \]

**Gross Margin** is the gross profit expressed as a percentage of the total revenue:

\[ \text{Gross Margin} = \frac{\text{gross income}}{\text{total revenue}} \]

**Example Calculation for the First Row:**

Given data:

- Unit Price: $45.79
- Quantity: 7

\[ \text{COGS} = 45.79 \times 7 = 320.53 \]

\[ \text{VAT} = 5\% \times 320.53 = 16.0265 \]

\[ \text{total} = 16.0265 + 320.53 = 336.5565 \]

\[ \text{Gross Margin Percentage} = \frac{16.0265}{336.5565} \approx 4.76\% \]

## Code

For the rest of the code, refer to the [SQL_queries.sql](https://github.com/Princekrampah/WalmartSalesAnalysis/blob/master/SQL_queries.sql) file

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
