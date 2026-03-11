# Restaurant-orders-data-analysis-using-SQL
# 🍽️ Restaurant Orders Data Analysis with SQL

This project analyzes restaurant order data using SQL to uncover insights about customer ordering behavior, sales performance, and menu popularity.

The goal is to answer practical business questions such as:

- Which menu items are ordered the most and least?
- Which orders generate the highest revenue?
- At what time of the day does the restaurant receive the most orders?
- Which cuisines contribute the most to sales?

The analysis is performed using SQL queries on two related tables: `menu_items` and `order_details`.

---

# 📂 Dataset Overview

The dataset contains two tables representing the restaurant's menu and customer orders.

## 1. menu_items

This table stores details about each menu item.

| Column | Description |
|------|-------------|
| menu_item_id | Unique identifier for each menu item |
| item_name | Name of the food item |
| category | Cuisine/category the item belongs to |
| price | Price of the menu item |

---

## 2. order_details

This table stores information about customer orders.

| Column | Description |
|------|-------------|
| order_details_id | Unique record ID |
| order_id | Identifier for each order |
| order_time | Time when the order was placed |
| item_id | Links the order to a menu item |

---

# 🔎 Business Questions & SQL Analysis

## 1️⃣ Most and Least Ordered Menu Items

This query counts how many times each item appears in customer orders.

```sql
SELECT m.item_name,
       COUNT(o.order_details_id) AS ordercount,
       m.category
FROM menu_items m, order_details o
GROUP BY m.item_name, m.category
ORDER BY ordercount DESC;
