# 🧑‍💼 SQL Problem 1378: Replace Employee ID With The Unique Identifier

## 📘 Table 1: `Employees`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| name          | varchar |
+---------------+---------+
```

- `id` is the **primary key**.
- Each row contains the **employee id** and **name**.

---

## 📘 Table 2: `EmployeeUNI`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| unique_id     | int     |
+---------------+---------+
```

- `(id, unique_id)` is the **composite primary key**.
- Each row maps an employee `id` to their `unique_id`.

---

## 🎯 Task

Write a SQL query to **replace the employee's id with their unique_id**, if available.  
If the employee **does not have a unique_id**, display `null`.

---

## 📥 Example Input

**Employees Table**

```
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
```

**EmployeeUNI Table**

```
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
```

---

## 📤 Example Output

```
+-----------+----------+
| unique_id | name     |
+-----------+----------+
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
+-----------+----------+
```

---

## ✅ SQL Solution

```sql
SELECT eu.unique_id, e.name 
FROM Employees e
LEFT JOIN EmployeeUNI eu
ON e.id = eu.id
ORDER BY name;
```

---

## 💬 Explanation

- We use a **LEFT JOIN** to combine both tables using `id`.
- `LEFT JOIN` ensures all employees are included even if no `unique_id` exists.
- If there’s **no match** in `EmployeeUNI`, the result will show `null` for `unique_id`.

---
