# TradeZone: SQL Business Analysis

## Project Overview

TradeZone is a fast-growing Nigerian e-commerce platform connecting buyers and sellers across **Lagos, Abuja, Kano, Port Harcourt, and Ibadan**.

As the platform grew between **2023 and 2024**, leadership became concerned that growth was masking underlying business problems, including declining customer retention, seller performance issues, and underperforming product categories.

This project was completed as a business-focused SQL analysis to help the **Head of Growth** and **Head of Seller Operations** understand what was happening across the platform ahead of the 2025 planning cycle.

I investigated eight business questions by first cleaning and validating the data, then translated the results into an analyst memo containing findings and recommendations.

---

## Business Problem

TradeZone's growth was not telling the full story.

The business needed to understand:

* Whether newly acquired customers were actually converting into buyers
* Which products were generating the most revenue
* Which sellers were fulfilling orders efficiently
* How revenue was changing between 2023 and 2024
* How customer spending was distributed
* Which payment methods customers preferred across different states
* Whether product ratings were associated with sales performance
* Which sellers qualified for a performance-based bonus

These questions formed the basis of the analysis.

---

## Dataset

The TradeZone database contains e-commerce data covering 2023–2024.

The dataset is made up of multiple relational tables, with the following sizes:

| Table         |  Rows |
| ------------- | ----: |
| Order Details | 2,155 |
| Orders        |   830 |
| Products      |    77 |
| Customers     |    91 |
| Employees     |     9 |
| Shippers      |     3 |
| Categories    |     8 |

The tables were connected through relationships between customers, orders, products, employees, categories, and shippers, allowing me to analyse TradeZone's sales and operational performance from multiple perspectives.

### Dataset Structure

| Table             | Key information                                            |
| ----------------- | ---------------------------------------------------------- |
| **Customers**     | Customer details and location                              |
| **Orders**        | Order-level sales and transaction information              |
| **Order Details** | Products, quantities, prices, and order-level line items   |
| **Products**      | Product names, categories, prices, and product information |
| **Categories**    | Product category information                               |
| **Employees**     | Employee information                                       |
| **Shippers**      | Shipping and fulfilment information                        |

The analysis was performed using **PostgreSQL**, with multiple tables joined together to answer the eight business questions.

---

# Part A: Data Cleaning & Preparation

Before conducting the business analysis, I cleaned and validated the dataset.

The cleaning process covered:

### Missing Values

I identified NULL and blank values in critical fields and determined how each should be handled before analysis.

### Duplicate Records

I checked the customer, seller, and order tables for duplicate records and removed duplicates where necessary.

### Inconsistent Formatting

I standardised:

* City names
* Date formats
* Product category names

Dates were standardised to **YYYY-MM-DD**, while product categories were normalised to title case.

### Data Validation

I also validated the consistency of the data by checking:

* Whether order totals matched the sum of their order items
* Orders where the difference exceeded **₦10**
* Review ratings outside the expected **1–5** range
* Negative product prices
* Discount percentages above **100%**

Any decisions made during the cleaning process were documented in SQL comments.

[Part 1.sql](https://github.com/user-attachments/files/33178518/Part.1.sql)


---

# Part B: Business Questions

## Q1. Customer Acquisition & 30-Day Conversion

**Business question:** Which five states acquired the most customers in 2024, and how many of those new customers made a purchase within their first 30 days?

For each of the top five states, I calculated:

* Number of new customer sign-ups
* Number of customers who made a purchase within 30 days
* 30-day conversion rate

**Why it matters:** Customer acquisition numbers alone do not show whether acquisition efforts are producing actual buyers. The conversion rate provides a clearer picture of the quality of new customer acquisition.

[Q1.sql](https://github.com/user-attachments/files/33178555/Q1.sql)


---

## Q2. Product Performance

**Business question:** Which products generated the most revenue in 2024?

I identified the **top 10 products by total revenue**, including:

* Product name
* Category
* Total revenue
* Total number of orders

Products were ranked by revenue in descending order.

**Why it matters:** Understanding which products generate the most revenue helps the business identify products that deserve greater attention when making inventory, promotion, and sales decisions.

[Q2.sql](https://github.com/user-attachments/files/33178596/Q2.sql)

---

## Q3. Seller Fulfilment Efficiency

**Business question:** Which sellers were the most efficient at fulfilling customer orders?

I calculated the average time between order placement and delivery for each seller and identified the **20 fastest sellers** among sellers who had completed at least 20 orders.

The analysis included:

* Total completed orders
* Average fulfilment time in hours
* Average customer rating

**Why it matters:** Fast fulfilment can contribute to a better customer experience. Comparing fulfilment time alongside customer ratings also provides context for understanding seller performance.

[Q3.sql](https://github.com/user-attachments/files/33178602/Q3.sql)

---

## Q4. Quarterly Revenue Trends

**Business question:** How did TradeZone's revenue performance change between 2023 and 2024?

For each quarter, I calculated:

* Total revenue
* Average order value
* Total number of orders

I then compared corresponding quarters across 2023 and 2024 to identify the quarter with the strongest revenue growth.

**Why it matters:** Looking at revenue by quarter helps leadership understand whether growth is consistent, seasonal, or concentrated in particular periods.

[Q4.sql](https://github.com/user-attachments/files/33178636/Q4.sql)

---

## Q5. Customer Spend Segmentation

**Business question:** How is customer spending distributed across TradeZone?

Customers were segmented according to their total 2024 spend:

| Segment         |          Spending |
| --------------- | ----------------: |
| High Spenders   |        ≥ ₦100,000 |
| Medium Spenders | ₦50,000 – ₦99,999 |
| Low Spenders    |         < ₦50,000 |

For each segment, I calculated:

* Customer count
* Average spend per customer
* Total revenue contribution

**Why it matters:** The number of customers alone does not tell the full story. Understanding how much revenue each segment contributes helps identify which customer groups have the greatest commercial importance.

[Q5.sql](https://github.com/user-attachments/files/33178660/Q5.sql)

---

## Q6. Payment Method Preferences by State

**Business question:** Which payment methods are most popular across TradeZone's different markets?

I analysed payment behaviour across each state using:

* Transaction count
* Total transaction amount
* Payment method

The analysis covered:

* Cash on Delivery
* Card
* Mobile Money
* Bank Transfer

I also identified the most popular payment method in each state.

**Why it matters:** Payment preferences can vary across markets. Understanding these differences can help TradeZone make better decisions around payment options and customer experience.

[Q6.sql](https://github.com/user-attachments/files/33178707/Q6.sql)

---

## Q7. Review Ratings & Sales Performance

**Business question:** How does product rating relate to sales performance?

Products were grouped into three rating categories:

| Rating Category | Average Rating |
| --------------- | -------------: |
| High Rated      |           4.0+ |
| Mid Rated       |     3.0 – 3.99 |
| Low Rated       |      Below 3.0 |

For each group, I calculated:

* Product count
* Total revenue
* Average unit price

**Why it matters:** Comparing sales performance across rating groups helps determine whether highly rated products are also contributing strongly to revenue.

[Q7.sql](https://github.com/user-attachments/files/33178743/Q7.sql)

---

## Q8. Top Seller Bonus Qualification

**Business question:** Which sellers qualified for a performance-based bonus?

I identified the **top 10 sellers by 2024 revenue** who met both requirements:

* At least 10 completed orders
* Average customer rating of 4.0 or above

The analysis included:

* Total orders
* Average customer rating
* Total revenue

**Why it matters:** This creates a data-based way of identifying high-performing sellers using both commercial performance and customer satisfaction.

[Q8.sql](https://github.com/user-attachments/files/33178756/Q8.sql)

---

# Key Analytical Themes

Across the eight questions, the analysis focused on four major areas of TradeZone's business:

### Customer Growth

Understanding whether new customer acquisition was translating into actual purchases.

### Product Performance

Identifying the products generating the most revenue and examining the relationship between product ratings and sales.

### Seller Operations

Evaluating fulfilment efficiency, customer ratings, and seller performance.

### Revenue & Customer Behaviour

Understanding revenue trends, customer spending patterns, and payment preferences across states.

---

# Analyst Memo

The SQL analysis was followed by a structured Analyst Memo addressed to the Head of Growth and Head of Seller Operations.

The memo translated the query results into:

* Executive summary
* Three key findings
* Two business recommendations
* Data quality notes
* Limitations of the available data

The recommendations were required to be directly traceable to the analysis rather than based on assumptions outside the dataset.

[Analyst_Memo.pdf](https://github.com/user-attachments/files/33178773/Analyst_Memo.pdf)
[cleaned_dump.sql](https://github.com/user-attachments/files/33178890/cleaned_dump.sql)


---
# Tools

**PostgreSQL**

Skills demonstrated:

* SQL data cleaning
* Data validation
* Relational data analysis
* Customer analytics
* Product analytics
* Seller performance analysis
* Revenue analysis
* Customer segmentation
* Business-focused reporting

---

# Project Outcome

This project strengthened my ability to approach SQL from a business perspective.

I had to determine what questions mattered to the business, validate the underlying data, investigate those questions using SQL, and communicate the results in a way that could support decisions.

The project therefore combined data preparation, SQL analysis, business interpretation, and recommendations into one end-to-end analytical workflow.





