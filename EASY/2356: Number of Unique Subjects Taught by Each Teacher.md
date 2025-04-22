# 🎓 SQL Problem 2356: Number of Unique Subjects Taught by Each Teacher

## 📘 Table: Teacher

| Column Name | Type |
|-------------|------|
| teacher_id  | int  |
| subject_id  | int  |
| dept_id     | int  |

- `(subject_id, dept_id)` is the **primary key**.
- Each row means a `teacher_id` teaches a `subject_id` in a `dept_id`.

---

## 🎯 Task

Write a query to calculate the **number of unique subjects** each teacher teaches in the university.

Return the result table in any order.

---

## 📥 Example Input

### Teacher

| teacher_id | subject_id | dept_id |
|------------|------------|---------|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |

---

## 📤 Expected Output

| teacher_id | cnt |
|------------|-----|
| 1          | 2   |
| 2          | 4   |

---

## ✅ SQL Solution

```sql
SELECT teacher_id , COUNT(DISTINCT(subject_id)) as cnt
FROM Teacher
GROUP BY teacher_id
```
