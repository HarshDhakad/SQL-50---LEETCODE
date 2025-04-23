# 🏢 LeetCode SQL Problem 1731: The Number of Employees Which Report to Each Employee

## 🧾 Table: Employees

| Column Name  | Type     |
|--------------|----------|
| employee_id  | int      |
| name         | varchar  |
| reports_to   | int      |
| age          | int      |

- **employee_id** is the primary key.
- Each employee may report to another employee via `reports_to`.
- Some employees have `NULL` in `reports_to`, meaning they **do not report to anyone**.

---

### ℹ️ Notes:
- A **manager** is defined as an employee **who has at least one other employee reporting to them**.
- You must return the manager’s:
  - `employee_id`
  - `name`
  - Number of direct reports
  - Average age of those direct reports (rounded to the nearest integer)

---

## 🎯 Task

Write a solution to **report the employee_id and name of all managers**, along with:

- The **number of employees** who report directly to them (`reports_count`)
- The **average age** of their reports (`average_age`), rounded to the nearest integer

Return the result **ordered by employee_id**.

---

## 📥 Example Input

### Employees Table

| employee_id | name    | reports_to | age |
|-------------|---------|------------|-----|
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |

---

## 📤 Expected Output

| employee_id | name  | reports_count | average_age |
|-------------|-------|---------------|-------------|
| 9           | Hercy | 2             | 39          |

---

## ✅ SQL Solution

```sql
SELECT e2.employee_id,e2.name,COUNT(*) as reports_count, ROUND(AVG(e1.age)) as average_age
FROM Employees e1 
JOIN Employees e2
ON e1.reports_to=e2.employee_id
GROUP BY e1.reports_to
ORDER BY e2.employee_id

```
