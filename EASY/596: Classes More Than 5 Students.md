# 🎓 SQL Problem 596: Classes More Than 5 Students

## 📘 Table: Courses

| Column Name | Type    |
|-------------|---------|
| student     | varchar |
| class       | varchar |

- `(student, class)` is the **primary key**.
- Each row shows a student and the class they're enrolled in.

---

## 🎯 Task

Write a query to find all the **classes that have at least 5 students**.

Return the result in any order.

---

## 📥 Example Input

### Courses

| student | class    |
|---------|----------|
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |

---

## 📤 Expected Output

| class   |
|---------|
| Math    |

---

## ✅ SQL Solution

```sql
SELECT class FROM Courses
GROUP BY class
HAVING COUNT(student)>=5
```
