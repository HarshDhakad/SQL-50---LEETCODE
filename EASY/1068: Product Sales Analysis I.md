# 🛒 SQL Problem 1068: Product Sales Analysis I

## 📘 Table 1: `Sales`

```
+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |
+-------------+-------+
```

- `(sale_id, year)` is the **composite primary key**.
- Each row shows the **sale** of a product in a given year.
- `price` is the **per-unit price**.

---

## 📘 Table 2: `Product`

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
+--------------+---------+
```

- `product_id` is the **primary key**.
- Each row links a **product ID** to its **name**.

---

## 🎯 Task

Write an SQL query to report the following **for each sale**:
- `product_name`
- `year`
- `price`

Return the result in **any order**.

---

## 📥 Example Input

**Sales Table**

```
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+ 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+
```

**Product Table**

```
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+
```

---

## 📤 Example Output

```
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+
```

---

## ✅ SQL Solution

```sql
SELECT 
    p.product_name,
    s.year,
    s.price
FROM Sales s
JOIN Product p 
    ON s.product_id = p.product_id;
```

---

## 💬 Explanation

- We're asked to **combine information** from both tables.
- The `Sales` table contains sales data, but only with `product_id`.
- The `Product` table has the **actual names** of products.
- So, we use a **JOIN** on `product_id` to get `product_name`.
- We then select the desired columns: `product_name`, `year`, and `price`.

---
