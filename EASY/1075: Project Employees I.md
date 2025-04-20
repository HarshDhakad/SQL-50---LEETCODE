# 🛠️ SQL Problem 1075: Project Employees I

## 📘 Tables

### 📁 Project

| Column Name | Type |
|-------------|------|
| project_id  | int  |
| employee_id | int  |

- `(project_id, employee_id)` is the **primary key**.
- `employee_id` is a foreign key from the `Employee` table.
- Shows which employee is working on which project.

---

### 👤 Employee

| Column Name      | Type    |
|------------------|---------|
| employee_id      | int     |
| name             | varchar |
| experience_years | int     |

- `employee_id` is the **primary key**.
- `experience_years` is **not NULL**.
- Shows details about each employee.

---

## 🎯 Task

Write a query to return the **average experience years** of employees **for each project**, **rounded to 2 decimal places**.

- Return the result in any order.
- Column name for average should be `average_years`.

---

## 📥 Example Input

### 📁 Project

| project_id | employee_id |
|------------|-------------|
| 1          | 1           |
| 1          | 2           |
| 1          | 3           |
| 2          | 1           |
| 2          | 4           |

### 👤 Employee

| employee_id | name   | experience_years |
|-------------|--------|------------------|
| 1           | Khaled | 3                |
| 2           | Ali    | 2                |
| 3           | John   | 1                |
| 4           | Doe    | 2                |

---

## 📤 Expected Output

| project_id | average_years |
|------------|----------------|
| 1          | 2.00           |
| 2          | 2.50           |

---

## ✅ SQL Solution

```sql

SELECT p.project_id,ROUND(AVG(e.experience_years),2) as average_years
FROM Project p 
LEFT JOIN Employee e
ON p.employee_id=e.employee_id
GROUP BY p.project_id
```

