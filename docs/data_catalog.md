# 📘 Data Catalog for Gold Layer

## Overview

The **Gold Layer** represents the business-level data model in the data warehouse.

It is designed to support analytics, reporting, and business intelligence use cases. The Gold Layer follows a **Star Schema** structure and includes dimension views and fact views.

---

## 1. gold.dim_customers

**Purpose:**  
Stores customer details enriched with demographic and geographic information.

| Column Name | Data Type | Description |
|---|---|---|
| customer_key | INT | Surrogate key uniquely identifying each customer record in the dimension view. |
| customer_id | INT | Unique numerical identifier assigned to each customer. |
| customer_number | NVARCHAR(50) | Alphanumeric identifier representing the customer, used for tracking and referencing. |
| first_name | NVARCHAR(50) | Customer's first name as recorded in the source system. |
| last_name | NVARCHAR(50) | Customer's last name or family name. |
| country | NVARCHAR(50) | Country of residence for the customer. |
| marital_status | NVARCHAR(50) | Marital status of the customer, such as Married or Single. |
| gender | NVARCHAR(50) | Gender of the customer, such as Male, Female, or n/a. |
| birthdate | DATE | Date of birth of the customer. |
| create_date | DATE | Date when the customer record was created in the source system. |

---

## 2. gold.dim_products

**Purpose:**  
Provides product information and product-related attributes for analytical reporting.

| Column Name | Data Type | Description |
|---|---|---|
| product_key | INT | Surrogate key uniquely identifying each product record in the dimension view. |
| product_id | INT | Unique identifier assigned to the product for internal tracking and referencing. |
| product_number | NVARCHAR(50) | Structured alphanumeric code representing the product. |
| product_name | NVARCHAR(50) | Descriptive name of the product, including details such as type, color, or size. |
| category_id | NVARCHAR(50) | Unique identifier for the product category. |
| category | NVARCHAR(50) | Broad classification of the product, such as Bikes or Components. |
| subcategory | NVARCHAR(50) | More detailed classification of the product within its category. |
| maintenance | NVARCHAR(50) | Indicates whether the product requires maintenance. |
| cost | INT | Cost or base price of the product. |
| product_line | NVARCHAR(50) | Product line or series to which the product belongs. |
| start_date | DATE | Date when the product became available for sale or use. |

---

## 3. gold.fact_sales

**Purpose:**  
Stores transactional sales data for analytical and reporting purposes.

| Column Name | Data Type | Description |
|---|---|---|
| order_number | NVARCHAR(50) | Unique alphanumeric identifier for each sales order. |
| product_key | INT | Surrogate key linking the sales record to the product dimension. |
| customer_key | INT | Surrogate key linking the sales record to the customer dimension. |
| order_date | DATE | Date when the order was placed. |
| shipping_date | DATE | Date when the order was shipped to the customer. |
| due_date | DATE | Date when the order payment or delivery was due. |
| sales_amount | INT | Total monetary value of the sale for the line item. |
| quantity | INT | Number of units ordered for the line item. |
| price | INT | Price per unit of the product. |

---

## Data Model Summary

The Gold Layer contains:

- **gold.dim_customers** — Customer dimension
- **gold.dim_products** — Product dimension
- **gold.fact_sales** — Sales fact table

The fact view connects to the dimension views using surrogate keys:

- `fact_sales.customer_key` → `dim_customers.customer_key`
- `fact_sales.product_key` → `dim_products.product_key`

This structure supports efficient analytical queries for customer behavior, product performance, and sales trends.
