# 🧪 SQL Problem 595: Big Countries

## 📘 Table: `World`

```
+-------------+-----------+
| Column Name | Type      |
+-------------+-----------+
| name        | varchar   |
| continent   | varchar   |
| area        | int       |
| population  | int       |
| gdp         | bigint    |
+-------------+-----------+
```

- `name` is the **primary key** (unique for each country).
- Each row contains:
  - `name` of the country
  - `continent` it belongs to
  - `area` in km²
  - `population`
  - `gdp` (Gross Domestic Product)

---

## 🎯 Task

A country is considered **big** if:

- It has an `area >= 3,000,000` km² **OR**
- It has a `population >= 25,000,000`

Write a SQL query to **find the `name`, `population`, and `area`** of all big countries.

Return the result **in any order**.

---

## 📥 Example Input

**World Table**

```
+-------------+-----------+---------+------------+--------------+
| name        | continent | area    | population | gdp          |
+-------------+-----------+---------+------------+--------------+
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |
+-------------+-----------+---------+------------+--------------+
```

---

## 📤 Example Output

```
+-------------+------------+---------+
| name        | population | area    |
+-------------+------------+---------+
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |
+-------------+------------+---------+
```

---

## 💡 Explanation

- **Afghanistan** is included because its population is greater than 25 million.
- **Algeria** is included because its population is over 25 million.
- Other countries do not satisfy either condition.

---

## ✅ SQL Solution

```sql
SELECT name, population, area FROM World
WHERE area >= 3000000 OR population >= 25000000;
```

