# 💼 SQL Problem 577: Employee Bonus

## 📘 Table 1: Employee

| Column Name | Type    |
|-------------|---------|
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |

- `empId` is the unique ID for each employee.
- Each row gives employee name, their ID, salary, and supervisor ID.

---

## 📘 Table 2: Bonus

| Column Name | Type |
|-------------|------|
| empId       | int  |
| bonus       | int  |

- `empId` is a foreign key referencing `Employee.empId`.
- Each row gives an employee's bonus amount.

---

## 🎯 Task

Return the **name and bonus** of each employee **whose bonus is less than 1000**, or who **did not receive any bonus** (i.e., `NULL`).

---

## 📥 Example Input

**Employee Table**

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

**Bonus Table**

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

---

## 📤 Example Output

| name  | bonus |
|-------|-------|
| Brad  | null  |
| John  | null  |
| Dan   | 500   |

---

## ✅ SQL Solution

```sql
SELECT e.name, b.bonus 
FROM Employee e LEFT JOIN Bonus b 
ON e.empId= b.empId
WHERE b.bonus IS NULL OR b.bonus < 1000;

```

---

## 💬 Explanation

- 🔗 LEFT JOIN is used to get all employees — even those without any bonus record.

-🧮 We use a WHERE clause to filter:

- - b.bonus IS NULL: Employee didn’t get any bonus.

- - b.bonus < 1000: Employee got a bonus, but it's less than 1000.

🎯 The final result shows the name and bonus amount of only those employees.

---
