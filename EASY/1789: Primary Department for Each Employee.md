# 🏢 LeetCode SQL Problem 1789: Primary Department for Each Employee

## 🧾 Table: Employee

| Column Name   | Type    |
|---------------|---------|
| employee_id   | int     |
| department_id | int     |
| primary_flag  | varchar |

- **Primary Key**: (employee_id, department_id)
- `employee_id` is the id of the employee.
- `department_id` is the id of the department.
- `primary_flag` is an ENUM: `'Y'` if the department is primary, `'N'` otherwise.

---

### ℹ️ Notes:
- An employee can be part of **multiple departments**.
- If an employee has **only one department**, the `primary_flag` is `'N'` but it should still be treated as their **primary department**.

---

## 🎯 Task

Write a solution to **report all the employees with their primary department**.

- If an employee has **only one department**, that department is the primary one (even if `primary_flag = 'N'`).

Return the result table in **any order**.

---

## 📥 Example Input

### Employee Table

| employee_id | department_id | primary_flag |
|-------------|----------------|--------------|
| 1           | 1              | N            |
| 2           | 1              | Y            |
| 2           | 2              | N            |
| 3           | 3              | N            |
| 4           | 2              | N            |
| 4           | 3              | Y            |
| 4           | 4              | N            |

---

## 📤 Expected Output

| employee_id | department_id |
|-------------|----------------|
| 1           | 1              |
| 2           | 1              |
| 3           | 3              |
| 4           | 3              |

---

## ✅ SQL Solution

```sql
SELECT employee_id,department_id 
FROM Employee
WHERE primary_flag='Y'
GROUP BY employee_id

UNION 

SELECT employee_id,department_id 
FROM Employee
GROUP BY employee_id
HAVING COUNT(*)=1 

```

---
### EXPLANATION
- This finds employees who are in only one department.

- Since COUNT(*) = 1, the employee has only one record.

- Combines the two results:

- - Employees with primary_flag='Y'

- - Employees who are in only one department
---
