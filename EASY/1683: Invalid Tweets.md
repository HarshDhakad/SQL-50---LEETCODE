# 🐦 SQL Problem 1683: Invalid Tweets

## 📘 Table: `Tweets`

```
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| tweet_id       | int     |
| content        | varchar |
+----------------+---------+
```

- `tweet_id` is the **primary key**.
- `content` contains only **alphanumeric characters**, `'!'`, and `' '` (spaces).
- This table records all tweets from a social media app.

---

## 🎯 Task

Write a SQL query to find the **IDs of invalid tweets**.

> A tweet is considered **invalid** if its `content` has **strictly more than 15 characters**.

Return the result table in **any order**.

---

## 📥 Example Input

**Tweets Table**

```
+----------+-----------------------------------+
| tweet_id | content                           |
+----------+-----------------------------------+
| 1        | Let us Code                       |
| 2        | More than fifteen chars are here! |
+----------+-----------------------------------+
```

---

## 📤 Example Output

```
+----------+
| tweet_id |
+----------+
| 2        |
+----------+
```

---

## 💡 Explanation

- Tweet `1` has 11 characters → ✅ Valid
- Tweet `2` has 33 characters → ❌ Invalid

---

## ✅ SQL Solution

```sql
SELECT tweet_id FROM Tweets
WHERE LENGTH(content) > 15;
```

---

## 🧠 Learning
- String length checking with `LENGTH()` or `CHAR_LENGTH()`
---
