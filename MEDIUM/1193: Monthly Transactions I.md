# 💳 LeetCode SQL Problem 1193: Monthly Transactions I

## 📘 Table: Transactions

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| country     | varchar |
| state       | enum    |
| amount      | int     |
| trans_date  | date    |

- `id` is the **primary key**.
- The table contains information about **incoming transactions**.
- `state` is an enum of type `["approved", "declined"]`.

---

## 🎯 Task

Write an SQL query to **find for each month and country**:
- Number of transactions
- Total amount of transactions
- Number of approved transactions
- Total amount of approved transactions

---

## 📥 Example Input

### Transactions Table

| id  | country | state    | amount | trans_date |
|-----|---------|----------|--------|------------|
| 121 | US      | approved | 1000   | 2018-12-18 |
| 122 | US      | declined | 2000   | 2018-12-19 |
| 123 | US      | approved | 2000   | 2019-01-01 |
| 124 | DE      | approved | 2000   | 2019-01-07 |

---

## 📤 Expected Output

| month    | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
|----------|---------|-------------|----------------|--------------------|-----------------------|
| 2018-12  | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01  | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01  | DE      | 1           | 1              | 2000               | 2000                  |

---

## ✅ SQL Solution
### USING LEFT FUNCTION
```sql
SELECT
LEFT(trans_date ,7) as month,
country ,
COUNT(id) as trans_count ,
SUM(IF(state='approved',1,0)) as approved_count ,
SUM(amount) as trans_total_amount ,
SUM(IF(state='approved',amount,0)) as approved_total_amount

FROM Transactions
GROUP BY month, country
```

### USING DATE_FORMAT FUNCTION
```sql
SELECT
DATE_FORMAT(trans_date, '%Y-%m') AS month,,
country ,
COUNT(id) as trans_count ,
SUM(IF(state='approved',1,0)) as approved_count ,
SUM(amount) as trans_total_amount ,
SUM(IF(state='approved',amount,0)) as approved_total_amount

FROM Transactions
GROUP BY month, country
```
---
# 💡 Explanation
- - DATE_FORMAT(trans_date, '%Y-%m') extracts the year and month.
  - LEFT(name,N) FUNCTION extracts the N characters from left.
- - COUNT(*) counts all transactions.

- - SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) counts only approved transactions.

- - SUM(amount) totals the transaction amounts.

- - SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) totals approved transaction amounts.

- - Group by month and country for accurate aggregation.

---
