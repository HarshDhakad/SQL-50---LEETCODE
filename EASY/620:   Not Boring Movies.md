# 🎬 SQL Problem 620: Not Boring Movies

## 📘 Table: Cinema

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| movie       | varchar |
| description | varchar |
| rating      | float   |

- `id` is the **primary key**.
- `rating` is a float with 2 decimal places, in the range [0, 10].
- Each row contains information about a movie.

---

## 🎯 Task

Return the movies that meet **both** of the following conditions:

1. `id` is **odd-numbered**
2. `description` is **not 'boring'**

📌 Sort the results by `rating` in **descending** order.

---

## 📥 Example Input

### 🎞️ Cinema

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | Fantacy     | 8.6    |
| 5  | House card | Interesting | 9.1    |

---

## 📤 Expected Output

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 5  | House card | Interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |

---

## ✅ SQL Solution

```sql
# Write your MySQL query statement below
SELECT * FROM Cinema
WHERE (id%2)!= 0 and description != 'boring'
ORDER BY rating DESC

```

-
