# 📊 SQL Problem 1729: Find Followers Count

## 📘 Table: Followers

| Column Name | Type |
|-------------|------|
| user_id     | int  |
| follower_id | int  |

- `(user_id, follower_id)` is the **primary key**.
- Each row means `follower_id` follows `user_id`.

---

## 🎯 Task

Write a SQL query to return the **number of followers** for each user.

Return the result **ordered by `user_id` in ascending order**.

---

## 📥 Example Input

### Followers

| user_id | follower_id |
|---------|-------------|
| 0       | 1           |
| 1       | 0           |
| 2       | 0           |
| 2       | 1           |

---

## 📤 Expected Output

| user_id | followers_count |
|---------|------------------|
| 0       | 1                |
| 1       | 1                |
| 2       | 2                |

---

## ✅ SQL Solution

```sql
SELECT user_id,COUNT(follower_id) as followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id
```
