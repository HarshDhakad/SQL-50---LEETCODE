## Problem 1341: Movie Rating

### Problem Statement

You are given three tables: `Movies`, `Users`, and `MovieRating`.

#### Tables

**Movies Table:**

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| title         | varchar |

- `movie_id` is the primary key for this table.
- `title` is the name of the movie.

**Users Table:**

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| name          | varchar |

- `user_id` is the primary key for this table.
- The column `name` contains unique values.

**MovieRating Table:**

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| user_id       | int     |
| rating        | int     |
| created_at    | date    |

- `(movie_id, user_id)` is the primary key for this table.
- `rating` is the user's rating for the movie.
- `created_at` is the date when the rating was created.

### Objective

1. Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.
2. Find the movie name with the highest average rating in February 2020. In case of a tie, return the lexicographically smaller movie name.

### Input Example

Movies table:

| movie_id    | title       |
|-------------|-------------|
| 1           | Avengers    |
| 2           | Frozen 2    |
| 3           | Joker       |

Users table:

| user_id     | name        |
|-------------|-------------|
| 1           | Daniel      |
| 2           | Monica      |
| 3           | Maria       |
| 4           | James       |

MovieRating table:

| movie_id    | user_id     | rating       | created_at  |
|-------------|-------------|--------------|-------------|
| 1           | 1           | 3            | 2020-01-12  |
| 1           | 2           | 4            | 2020-02-11  |
| 1           | 3           | 2            | 2020-02-12  |
| 1           | 4           | 1            | 2020-01-01  |
| 2           | 1           | 5            | 2020-02-17  | 
| 2           | 2           | 2            | 2020-02-01  | 
| 2           | 3           | 2            | 2020-03-01  |
| 3           | 1           | 3            | 2020-02-22  | 
| 3           | 2           | 4            | 2020-02-25  |

### Output Example

| results      |
|--------------|
| Daniel       |
| Frozen 2     |

### Explanation

- **Daniel** and **Monica** have rated 3 movies ("Avengers", "Frozen 2", and "Joker"), but **Daniel** is lexicographically smaller.
- **Frozen 2** and **Joker** have an average rating of 3.5 in February, but **Frozen 2** is lexicographically smaller.

### Solution
❌ Query
```sql
-- SELECT name as results FROM MovieRating m
-- INNER JOIN Users u
-- ON m.user_id=u.user_id
-- GROUP BY m.user_id
-- ORDER BY COUNT(*) DESC
-- LIMIT 1

-- UNION ALL

-- SELECT title as results FROM MovieRating m
-- INNER JOIN Movies mo
-- ON mo.movie_id=m.movie_id
-- WHERE MONTH(created_at)=2 AND YEAR(created_at)=2020
-- GROUP BY m.movie_id
-- ORDER BY AVG(rating) DESC,mo.title
-- LIMIT 1
```
-- Problem: UNION can't have ORDER BY or LIMIT in individual SELECTs
✅ Query
```sql
SELECT results FROM (
    SELECT name AS results
    FROM MovieRating m
    INNER JOIN Users u ON m.user_id = u.user_id
    GROUP BY m.user_id
    ORDER BY COUNT(*) DESC,name
    LIMIT 1
) AS TopUser

UNION ALL

SELECT results FROM (
    SELECT title AS results
    FROM MovieRating m
    INNER JOIN Movies mo ON mo.movie_id = m.movie_id
    WHERE MONTH(created_at) = 2 AND YEAR(created_at) = 2020
    GROUP BY m.movie_id
    ORDER BY AVG(rating) DESC, mo.title
    LIMIT 1
) AS TopMovie;

```
