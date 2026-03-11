# 🍽️ Restaurant Orders Data Analysis (SQL)

## Project Overview

This project analyzes restaurant order data using SQL to uncover insights about customer ordering behavior, menu performance, and revenue trends.

The objective of this analysis is to answer key business questions that can help a restaurant improve decision-making around:

- Menu optimization
- Customer demand patterns
- Revenue generation
- Operational planning

The analysis is performed using SQL queries on two relational tables: **menu_items** and **order_details**.

---

# 📂 Dataset Description

## 1. menu_items

This table contains details about the restaurant’s menu items.

| Column | Description |
|------|-------------|
| menu_item_id | Unique identifier for each menu item |
| item_name | Name of the menu item |
| category | Cuisine or food category |
| price | Price of the item |

---

## 2. order_details

This table contains transaction-level information about customer orders.

| Column | Description |
|------|-------------|
| order_details_id | Unique ID for each record |
| order_id | Unique identifier for each order |
| order_time | Time the order was placed |
| item_id | ID linking the order to a menu item |

---

# 🔎 Business Questions, Analysis & Insights

## 1️⃣ What are the most and least ordered items?

```sql
SELECT m.item_name,
       COUNT(o.order_details_id) AS ordercount,
       m.category
FROM menu_items m, order_details o
GROUP BY m.item_name, m.category
ORDER BY ordercount DESC;
```

### Analysis

This query counts how many times each menu item appears in customer orders.

### Insights

- Items appearing at the top of the result represent the **most frequently ordered dishes**, indicating strong customer demand.
- These items are likely **customer favorites** and should remain prominent on the menu.
- Items with low order counts may indicate **low popularity, pricing issues, or poor menu placement**.
- The restaurant may consider **removing, revising, or promoting underperforming items**.

---

## 💰 2️⃣ What do the highest spend orders look like?

```sql
SELECT m.item_name,
       m.category,
       SUM(m.price) AS sales,
       o.order_id
FROM menu_items m, order_details o
GROUP BY m.item_name, m.category, o.order_id
ORDER BY sales DESC
LIMIT 10;
```

### Analysis

This query calculates the total value of items purchased within each order.

### Insights

- High-value orders often include **multiple items or higher-priced menu options**.
- Identifying these orders helps understand **customer spending patterns**.
- Items frequently appearing in high-value orders could be:
  - Featured in promotions
  - Bundled into meal deals
  - Highlighted as premium offerings.

---

## ⏰ 3️⃣ Are there certain times that have more or fewer orders?

```sql
SELECT COUNT(o.order_details_id) AS ordercount,
       EXTRACT(HOUR FROM o.order_time) AS time
FROM order_details o
GROUP BY time
ORDER BY ordercount DESC;
```

### Analysis

This query extracts the hour from each order time and counts the number of orders placed during each hour.

### Insights

- Hours with the highest order counts represent **peak demand periods**.
- These times likely correspond to **lunch or dinner rush hours**.
- Restaurants can use this information to:
  - Schedule **more staff during busy periods**
  - Prepare ingredients ahead of time
  - Improve service efficiency during peak hours.

---

## 🍜 Which cuisines should the restaurant focus on developing more menu items for?

```sql
SELECT m.item_name,
       m.category,
       SUM(m.price) AS sales,
       COUNT(o.order_details_id) AS ordercount
FROM menu_items m, order_details o
GROUP BY item_name, category, order_id
ORDER BY sales DESC;
```

### Analysis

This query measures both **total revenue generated** and **order frequency** for menu items.

### Insights

- Items generating both **high sales and high order counts** are the restaurant’s **best-performing menu items**.
- Categories appearing frequently among top results suggest **strong customer preference for those cuisines**.
- The restaurant could consider:
  - Expanding these cuisines by introducing new dishes
  - Creating promotions around these popular categories
  - Featuring them more prominently on the menu.

---

## 🕒 What time does the restaurant make the most sales?

```sql
SELECT EXTRACT(HOUR FROM order_time) AS time,
       SUM(m.price) AS sales
FROM order_details o, menu_items m
GROUP BY time
ORDER BY sales DESC;
```

### Analysis

This query calculates the total revenue generated during each hour of the day.

### Insights

- The hour with the highest sales represents the **most profitable time of the day**.
- This may differ from the hour with the most orders if customers tend to buy **higher-priced items at certain times**.
- The restaurant can use this insight to:
  - Increase staffing during peak revenue hours
  - Introduce promotions during slower periods
  - Optimize kitchen preparation schedules.

---

# 🧠 SQL Skills Demonstrated

This project demonstrates several SQL concepts including:

- Data aggregation using **COUNT()** and **SUM()**
- Data grouping using **GROUP BY**
- Sorting results using **ORDER BY**
- Limiting results using **LIMIT**
- Extracting time values using **EXTRACT()**
- Working with multiple tables to generate insights

---

# 🚀 How to Run This Project

1. Clone the repository

```
git clone https://github.com/yourusername/restaurant-orders-analysis.git
```

2. Import the dataset into your SQL environment (PostgreSQL, MySQL, or any SQL client).

3. Run the SQL queries provided in the project to reproduce the analysis.

---

# 📊 Project Outcome

Through SQL analysis of restaurant order data, this project demonstrates how raw transactional data can be transformed into actionable insights that support:

- Menu optimization
- Revenue analysis
- Customer behavior understanding
- Operational decision-making
