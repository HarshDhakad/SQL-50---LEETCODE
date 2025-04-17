# 👥 SQL Problem 1581: Customer Who Visited but Did Not Make Any Transactions

## 📘 Table 1: `Visits`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| visit_id    | int     |
| customer_id | int     |
+-------------+---------+
```

- `visit_id` is unique for each visit.
- Each row shows a **customer’s visit** to the mall.

---

## 📘 Table 2: `Transactions`

```
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| transaction_id | int     |
| visit_id       | int     |
| amount         | int     |
+----------------+---------+
```

- Each row is a **purchase** made during a `visit_id`.
- One visit can have **multiple transactions**, or none at all.

---

## 🎯 Task

Find:
- The IDs of **customers who visited the mall** but **did NOT make any transactions**.
- Count **how many such visits** were made by each customer.

---

## 📥 Example Input

**Visits**

```
+----------+-------------+
| visit_id | customer_id |
+----------+-------------+
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |
+----------+-------------+
```

**Transactions**

```
+----------------+----------+--------+
| transaction_id | visit_id | amount |
+----------------+----------+--------+
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |
+----------------+----------+--------+
```

---

## 📤 Example Output

```
+-------------+----------------+
| customer_id | count_no_trans |
+-------------+----------------+
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |
+-------------+----------------+
```

---

## ✅ SQL Solution

```sql
SELECT 
    v.customer_id,
    COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t 
    ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

---

## 💬 Explanation

- We use a `LEFT JOIN` to keep **all visits**, and bring in transaction data if present.
- For visits **without any transactions**, the `transaction_id` will be `NULL`.
- We filter out only those rows using `WHERE t.transaction_id IS NULL`.
- Finally, we **group by `customer_id`** and **count** how many such visits they had.

---

