# 👥 SQL Problem 570: Managers with at Least 5 Direct Reports

## 📘 Table: Employee

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

- `id` is the **primary key**.
- `managerId` refers to the `id` of another employee (can be `NULL` if they don’t have a manager).
- An employee **cannot** be their own manager.

---

## 🎯 Task

Find the **names of managers** who have **at least five direct reports**.

- A direct report is an employee whose `managerId` matches the `id` of a manager.
- Return the result table in **any order**.

---

## 📥 Example Input

### 👤 Employee

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

---

## 📤 Expected Output

| name |
|------|
| John |

---

## ✅ SQL Solution

```sql
SELECT e1.name FROM Employee e1
JOIN Employee e2 
ON e1.id = e2.managerId
GROUP BY e2.managerId
HAVING COUNT(e2.managerId) >= 5;

```


---

## 📤 Explanation

- Join the Employee table with itself: e1 (manager) and e2 (employee).

- Group by managerId and count employees.

- Filter managers with 5 or more reports using HAVING.
---
