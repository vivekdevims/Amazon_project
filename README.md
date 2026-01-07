# Amazon-Sales-Analysis-SQL-Project
This is SQL based project in which user has created database and added multiple tables to perform analysis on amazon dataset using various SQL functions &amp; methods

<img width="1200" height="363" alt="image" src="https://github.com/user-attachments/assets/2f4c7554-ced9-4697-8937-e6d8c9910847" />

---

## *Project Overview*
Analyzed a dataset of over 20,000 sales records from an Amazon-like e-commerce platform using PostgreSQL. This project involved extensive querying to understand customer behavior, product performance, and sales trends. Through it, I tackled various SQL challenges, including revenue analysis, customer segmentation, and inventory management.

The project also emphasized data cleaning, managing null values, and applying structured queries to solve real-world business problems.

An ERD diagram was created to provide a clear visual representation of the database schema and table relationships.

<img width="869" height="555" alt="ERD" src="https://github.com/user-attachments/assets/4f8f178f-59b2-42e4-b7c9-8194c2aceaac" />

---

## *Objective*

The primary objective of this project is to showcase SQL proficiency through complex queries that address real-world e-commerce business challenges. The analysis covers various aspects of e-commerce operations

## *SQL Concepts Used*
Joins , case statements , window functions - Rank , Dense Rank , Lag , Group By , Having , Subqueries.

## *Key Insights*
High-Value Customers: The top 10 customers contribute significantly to the overall revenue, indicating the importance of customer retention strategies.

Payment Efficiency: The payment success rate provides insights into the reliability of the payment processing system.

Product Performance: Identifying top-selling products helps in inventory management and marketing focus.

Return Rates: Products with high return rates may require quality assessment or better customer education.

Seller Contributions: Understanding which sellers generate the most revenue can inform partnership and commission strategies.

## *Database Setup & Design*

## *Schema Structure*
```sql
CREATE DATABASE AMAZON_PROJECT;
USE AMAZON_PROJECT;


-- customer
select * from customers;

-- rename column name
ALTER TABLE customers
RENAME COLUMN Customer_id TO customer_id;

-- check duplicate values
SELECT customer_id, COUNT(*)
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;

-- ASSIGN PRIMARY KEY
ALTER TABLE customers
add constraint pk_customers
primary key (Customer_id);

-- CATEGORY TABLE
SELECT * FROM CATEGORY;

-- RENAME COLUMN
ALTER TABLE category
RENAME COLUMN Category_id TO category_id;

-- ASSIGN KEY
ALTER TABLE category
add constraint pk_category
primary key (Category_id);

-- 
SET SQL_SAFE_UPDATES = 0;
UPDATE category
SET category_name =  CONCAT(
        UPPER(SUBSTRING(category_name, 1, 1)),
        LOWER(SUBSTRING(category_name, 2))
    );
SET SQL_SAFE_UPDATES = 1;

-- SELLERS TABLE
SELECT * FROM SELLERS;

-- RENAME SELLERS
ALTER TABLE SELLERS
RENAME COLUMN ï»¿seller_id TO seller_id;

-- ASSIGN KEY
ALTER TABLE sellers
add constraint pk_sellers
primary key (seller_id);

-- PRODUCTS TABLE
SELECT * FROM products;

-- ASSIGN PRIMARY KEY AND FOREIGN KEY
ALTER TABLE products
ADD CONSTRAINT pk_products
primary key (product_id);

ALTER TABLE products
ADD CONSTRAINT fk_products_category
FOREIGN KEY (category_id) REFERENCES category(category_id);

-- ORDERS
SELECT * FROM orders;

-- RENAME COLUMN
ALTER TABLE orders
RENAME COLUMN ï»¿order_id to order_id;

-- ASSIGN PRIMARY KEY AND FOREIGN KEY
ALTER TABLE orders
ADD CONSTRAINT pk_orders
PRIMARY KEY (order_id);

ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
FOREIGN KEY(customer_id) REFERENCES customers(customer_id);

-- ORDER_ITEMS
SELECT * FROM order_items;

-- RENAME COLUMNS
ALTER TABLE order_items
RENAME COLUMN ï»¿order_item_id to order_item_id;

-- ASSIGN PRIMARY KEY 
ALTER TABLE order_items
ADD CONSTRAINT pk_order_items
PRIMARY KEY (order_item_id);

-- ASSIGN FOREIGN KEY
ALTER TABLE order_items
ADD CONSTRAINT fk_order_item
FOREIGN KEY (order_id) REFERENCES orders(order_id);

ALTER TABLE order_items
ADD CONSTRAINT fk_order_item_product
FOREIGN KEY (product_id) REFERENCES products(product_id);

-- ADD NEW COLUMN
ALTER table order_items
ADD column total_sale float;
SET SQL_SAFE_UPDATES = 0;
UPDATE order_items
SET total_sale= quantity * price_per_unit;
SET SQL_SAFE_UPDATES = 1;
-- PAYMENTS TABLE
SELECT * FROM payments;

-- RENAME COLUMN
ALTER TABLE PAYMENTS
RENAME COLUMN ï»¿payment_id to payment_id;

-- ASSIGN KEY 
ALTER TABLE payments
ADD CONSTRAINT PK_PAYMENT_ID
PRIMARY KEY (payment_id);

-- ASSIGN FOREIGN KEY
ALTER TABLE payments
ADD CONSTRAINT FK_PAYMENTS_ORDER
FOREIGN KEY (order_id) REFERENCES orders(order_id);

-- SHIPPING TABLE
SELECT * FROM SHIPPING;
-- RENAME COLUMN
ALTER TABLE SHIPPING
RENAME COLUMN ï»¿shipping_id TO shipping_id;

-- ASSIGN PRIMARY KEY AND FOREIGN KEY
ALTER table shipping
ADD CONSTRAINT pk_shipping
PRIMARY KEY (shipping_id);

ALTER table shipping
ADD CONSTRAINT fk_shipping_order
FOREIGN KEY (order_id) REFERENCES orders(order_id);

-- inventory table
select * from inventory;

-- RENAME COLUMN
ALTER TABLE inventory
RENAME COLUMN ï»¿inventory_id TO inventory_id;

-- ASSIGN PRIMARY KEY
ALTER TABLE inventory
add constraint pk_inventory
primary key (inventory_id);

-- ASSIGN FOREIGN KEY
ALTER TABLE inventory
ADD CONSTRAINT fk_inventory_product
foreign key(product_id) references products(product_id);

  );
```
