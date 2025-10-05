# Week-8 Assignment-Final-Project

🛒 E-commerce Database Management System (MySQL)
📘 Overview

This project implements a complete relational database schema for an E-commerce Management System using MySQL.
It includes all the core entities, relationships, and constraints required for real-world online store functionality — from users, products, and orders to payments, shipments, and reviews.

The design follows best practices of relational modeling:

Proper normalization (up to 3NF+)

Referential integrity (foreign key constraints)

Indexing for performance

One-to-One, One-to-Many, and Many-to-Many relationships

Data validation through CHECK constraints

Optional triggers for automation

🎯 Objectives

Demonstrate the ability to design and implement a relational database from scratch.

Showcase the use of primary keys, foreign keys, and relationships.

Implement data integrity, referential constraints, and normalization.

Prepare a ready-to-use schema for connecting to backend APIs (e.g., Node.js, FastAPI).

🏗️ Database Schema Summary

Database Name: ecommerce_db
Character Set: utf8mb4
Engine: InnoDB

📂 Main Entities
Table	Description	Relationship Type
users	Stores account and login info	Primary entity
user_profiles	Extended user info	1:1 with users
addresses	User shipping/billing addresses	1:N from users
categories	Product grouping hierarchy	Self-referencing (parent-child)
products	Product catalog	Core entity
product_images	Images for each product	1:N from products
product_categories	Product–Category mapping	M:N
suppliers	Product suppliers	Core entity
product_suppliers	Product–Supplier mapping	M:N
warehouses	Stock storage locations	Core entity
inventory	Product stock tracking per warehouse	1:N
coupons	Discount rules	Optional reference in orders
orders	Customer orders	Linked to users, addresses, coupons
order_items	Line items in each order	1:N from orders
payments	Transaction records per order	1:N
shipments	Shipping tracking details	1:1 or 1:N from orders
product_reviews	Customer product feedback	User + Product relationship
carts	Active user carts	1:1 with users
cart_items	Products in cart	1:N from carts
wishlists	User wishlists	1:N
wishlist_items	Products saved in wishlists	M:N
🔑 Relationship Highlights

One-to-One:

users → user_profiles

One-to-Many:

users → addresses, orders, carts, wishlists

products → product_images, product_reviews

orders → order_items, payments, shipments

Many-to-Many:

products ↔ categories (via product_categories)

products ↔ suppliers (via product_suppliers)

wishlists ↔ products (via wishlist_items)

⚙️ Setup Instructions
1️⃣ Prerequisites

Install MySQL 8.0+

Have access to a MySQL client (CLI, Workbench, or VS Code extension)

2️⃣ Create and Populate Database

Run the SQL script in your MySQL client:

mysql -u root -p < ecommerce_db.sql


This will:

Drop any existing ecommerce_db

Create a new database

Create all tables, constraints, and indexes

You can verify by running:

USE ecommerce_db;
SHOW TABLES;

🧠 Design Notes
✅ Normalization

The schema follows Third Normal Form (3NF).

Redundancy is minimized through reference tables (e.g., suppliers, categories).

Composite keys and M:N join tables are properly implemented.

🧩 Constraints

Primary Keys: Enforce uniqueness.

Foreign Keys: Maintain referential integrity with CASCADE and SET NULL rules.

CHECK Constraints: Validate prices, quantities, and ratings.

UNIQUE Constraints: Prevent duplicate entries (emails, SKUs, etc.).

ENUM Types: Restrict values for fields like gender, order_status, and payment_method.

⚡ Indexes

Optimized indexes exist for high-frequency query columns:

products.name, products.price

orders.user_id

order_items.order_id

inventory.product_id

💾 Example Use Cases

User creates account: inserts into users, user_profiles

User places order: inserts into orders and order_items

Admin updates inventory: modifies inventory.quantity

Customer reviews a product: inserts into product_reviews

Cart & Wishlist: carts and wishlists track user-selected items

🧰 Integration Ready

This schema can be directly connected to:

FastAPI or Flask (Python)

Express.js (Node.js)

Laravel or Django ORM

Spring Boot (Java) or .NET Entity Framework

Example DSN:

mysql+pymysql://root:password@localhost/ecommerce_db

🔒 Data Integrity Features

Foreign keys with CASCADE on deletes (maintains relational cleanup)

CHECK constraints prevent invalid numeric and enum data

UNIQUE indexes ensure data consistency (e.g., only one active cart per user)

Optional triggers (commented for safety) can maintain audit timestamps

📊 Entity Relationship Diagram (ERD)

(Optional for submission — you can include an ERD screenshot here.)

Example structure:

Users → Orders → Order_Items → Products → Categories
Users → Carts → Cart_Items → Products
Products → Suppliers (M:N)
Products → Reviews (1:N)
Orders → Payments, Shipments




