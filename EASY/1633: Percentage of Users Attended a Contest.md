# 📊 SQL Problem 1633: Percentage of Users Attended a Contest

## 📘 Tables

### Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| user_name   | varchar |

### Register

| Column Name | Type |
|-------------|------|
| contest_id  | int  |
| user_id     | int  |

- `user_id` is the primary key in `Users`.
- `(contest_id, user_id)` is the primary key in `Register`.

---

## 🎯 Task

Find the **percentage of users** who registered in each contest, **rounded to two decimals**.

- Return the result ordered by `percentage` in **descending** order.
- In case of tie, order by `contest_id` in **ascending** order.

---

## 📥 Example Input

### Users

| user_id | user_name |
|---------|-----------|
| 6       | Alice     |
| 2       | Bob       |
| 7       | Alex      |

### Register

| contest_id | user_id |
|------------|---------|
| 215        | 6       |
| 209        | 2       |
| 208        | 2       |
| 210        | 6       |
| 208        | 6       |
| 209        | 7       |
| 209        | 6       |
| 215        | 7       |
| 208        | 7       |
| 210        | 2       |
| 207        | 2       |
| 210        | 7       |

---

## 📤 Expected Output

| contest_id | percentage |
|------------|------------|
| 208        | 100.0      |
| 209        | 100.0      |
| 210        | 100.0      |
| 215        | 66.67      |
| 207        | 33.33      |

---

## ✅ SQL Solution

```sql
SELECT contest_id, 
ROUND(COUNT(DISTINCT(user_id))/ (SELECT COUNT(*) FROM Users)*100,2) as percentage
FROM Register
GROUP BY contest_id
ORDER BY percentage DESC,contest_id ASC

```
---
## EXPLANATION
- - Simple Subquery is used for extracting the count of users
---
