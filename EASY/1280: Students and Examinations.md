# 🎓 SQL Problem 1280: Students and Examinations

## 📘 Table 1: Students

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| student_name | varchar |

- `student_id` is the **primary key**.
- Each row represents a student.

---

## 📘 Table 2: Subjects

| Column Name  | Type    |
|--------------|---------|
| subject_name | varchar |

- `subject_name` is the **primary key**.
- Each row represents a school subject.

---

## 📘 Table 3: Examinations

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| subject_name | varchar |

- No primary key.
- Multiple entries indicate a student attended that exam multiple times.
- Each student from the Students table takes every course from the Subjects table.

---

## 🎯 Task

Report how many times **each student** attended **each subject's exam**.

### ➕ If a student **never attended** an exam for a subject, the count should be **0**.

- Return results ordered by `student_id` and `subject_name`.

---

## 📥 Example Input

### 🧑 Students

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

### 📚 Subjects

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

### 📝 Examinations

| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

---

## 📤 Expected Output

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

---

## ✅ SQL Solution

```sql
SELECT 
    s.student_id,
    s.student_name,
    sub.subject_name,
    COUNT(e.subject_name) AS attended_exams
FROM Students s
CROSS JOIN Subjects sub
LEFT JOIN Examinations e
    ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;


```

---
# Explanation

- - Each student from the Students table takes every course from the Subjects table
  - This line indicates CROSS JOIN in Students and Subjects Table
- - We want all student and its subjects even he/she didn't attend exam
  - so we LEFT JOIN with Examination table
  -  ON s.student_id = e.student_id -> this for join condition for student and examination table
  -   sub.subject_name = e.subject_name -> this for join condition for subject and examination table
- - Then Group BY with s.student_id, s.student_name, sub.subject_name due to COUNT aggregate function
- - And at last ORDER BY student id and subject name


---
