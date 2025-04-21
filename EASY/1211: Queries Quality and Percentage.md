# 📊 SQL Problem 1211: Queries Quality and Percentage

## 📘 Table: Queries

| Column Name | Type    |
|-------------|---------|
| query_name  | varchar |
| result      | varchar |
| position    | int     |
| rating      | int     |

- This table may have duplicate rows.
- The `position` ranges from 1 to 500.
- The `rating` ranges from 1 to 5.
- Queries with rating < 3 are considered **poor queries**.

---

## 🎯 Task

Write a solution to find:
- Each `query_name`
- The **quality**, defined as the average of `(rating / position)`
- The **poor_query_percentage**, defined as the percentage of queries with rating < 3

Both `quality` and `poor_query_percentage` should be **rounded to two decimal places**.

---

## 📥 Example Input

### Queries

| query_name | result           | position | rating |
|------------|------------------|----------|--------|
| Dog        | Golden Retriever | 1        | 5      |
| Dog        | German Shepherd  | 2        | 5      |
| Dog        | Mule             | 200      | 1      |
| Cat        | Shirazi          | 5        | 2      |
| Cat        | Siamese          | 3        | 3      |
| Cat        | Sphynx           | 7        | 4      |

---

## 📤 Expected Output

| query_name | quality | poor_query_percentage |
|------------|---------|-----------------------|
| Dog        | 2.50    | 33.33                 |
| Cat        | 0.66    | 33.33                 |

---

## ✅ SQL Solution

### BY SUBQUERY->

```sql
SELECT a.query_name ,
ROUND(AVG(a.rating/a.position),2) as quality , 
ROUND(((SELECT COUNT(*) FROM Queries b WHERE b.query_name=a.query_name AND b.rating<3)/COUNT(a.query_name))*100,2) as poor_query_percentage
FROM Queries a
GROUP BY a.query_name
```
### BY IF CONDITION (OPTIMAL)
```sql
SELECT a.query_name ,
ROUND(AVG(a.rating/a.position),2) as quality , 
ROUND(AVG(IF(rating<3,1,0))*100,2) as poor_query_percentage
FROM Queries a
GROUP BY a.query_name
```
