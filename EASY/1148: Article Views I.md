# 📚 SQL Problem 1148: Article Views I

## 📘 Table: `Views`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |
+---------------+---------+
```

- There is **no primary key**, so duplicate rows may exist.
- Each row records that a `viewer_id` viewed an article written by `author_id` on `view_date`.
- If `author_id == viewer_id`, it means the **author viewed their own article**.

---

## 🎯 Task

Write a SQL query to find **all authors** who have **viewed at least one of their own articles**.

Return the result table **sorted by `id` in ascending order**.

---

## 📥 Example Input

**Views Table**

```
+------------+-----------+-----------+------------+
| article_id | author_id | viewer_id | view_date  |
+------------+-----------+-----------+------------+
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |
+------------+-----------+-----------+------------+
```

---

## 📤 Example Output

```
+------+
| id   |
+------+
| 4    |
| 7    |
+------+
```

---

## 💡 Explanation

- Author `7` viewed their own article (row 3).
- Author `4` viewed their own article (row 6 and 7).
- Author `3` **did not** view their own article (only viewers `5` and `6`).

---

## ✅ SQL Solution

```sql
SELECT DISTINCT author_id AS id FROM Views
WHERE author_id = viewer_id
ORDER BY author_id;
```

