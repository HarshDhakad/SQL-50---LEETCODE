# 🔢 LeetCode SQL Problem 619: Biggest Single Number

## 🧾 Table: MyNumbers

| Column Name | Type |
|-------------|------|
| num         | int  |

- This table **may contain duplicates** (no primary key).
- Each row contains an integer value.

---

### ℹ️ Notes:
- A **single number** is a number that appears **only once** in the table.
- You need to find the **largest single number**.
- If no single number exists, return **null**.

---

## 🎯 Task

Write a solution to **find the largest single number** from the table.

- Return `null` if no such number exists.

---

## 📥 Example Input

### MyNumbers Table

| num |
|-----|
| 8   |
| 8   |
| 3   |
| 3   |
| 1   |
| 4   |
| 5   |
| 6   |

---

## 📤 Expected Output

| num |
|-----|
| 6   |

---

### 🧠 Explanation:
- Single numbers are: **1, 4, 5, 6**
- The **largest** among them is **6**, so we return 6.

---

## ✅ SQL Solution

```sql
SELECT MAX(num) as num FROM  (SELECT num FROM MyNumbers 
GROUP BY num
HAVING COUNT(*)=1) as UniqueNumbers;
```

---
## TIPS->

- It is mandatory to alias the subquery table
---
