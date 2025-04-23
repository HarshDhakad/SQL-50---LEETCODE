# 🔺 LeetCode SQL Problem 610: Triangle Judgement

## 🧾 Table: Triangle

| Column Name | Type |
|-------------|------|
| x           | int  |
| y           | int  |
| z           | int  |

- **Primary Key**: (x, y, z)
- Each row contains three line segment lengths.

---

## 🎯 Task

Write an SQL query to **report whether the three segments can form a triangle**.

Return the result table in **any order**.

---

## 📥 Example Input

### Triangle Table

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

---

## 📤 Expected Output

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

---

## ✅ SQL Solution

```sql
SELECT x,y,z, IF(x+y>z AND x+z>y AND y+z>x,'Yes','No') as triangle
FROM Triangle
```
