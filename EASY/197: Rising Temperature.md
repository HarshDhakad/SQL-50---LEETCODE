# 🌡️ Leetcode 197: Rising Temperature

---

## 📄 Problem Statement

You are given a table named `Weather` that stores daily temperature records. The table is structured as follows:

**Table: Weather**

| Column Name   | Type  |
|---------------|-------|
| id            | int   |
| recordDate    | date  |
| temperature   | int   |

- `id` is the unique identifier for each entry.
- Each `recordDate` is unique — there are no two records for the same day.

### ❓ Task

Find the **IDs of all dates** where the **temperature was higher** than the **previous day**.

---

## 🧪 Example

### Input:

**Weather Table:**

| id | recordDate | temperature |
|----|------------|-------------|
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |

### Output:

| id |
|----|
| 2  |
| 4  |

### 🔍 Explanation:

- On **2015-01-02**, temperature rose from **10 → 25**, so we include id **2**
- On **2015-01-04**, temperature rose from **20 → 30**, so we include id **4**

---

## 💡 SQL Solution

```sql
SELECT b.id AS id
FROM Weather a JOIN Weather b
ON DATEDIFF(a.recordDate, b.recordDate) = -1
AND a.temperature < b.temperature;
```


## 💬 Explanation

- **JOIN**: This query uses a self-join between the `Weather` table, aliasing it as `a` and `b`.
- **DATEDIFF**: The `DATEDIFF(a.recordDate, b.recordDate) = -1` condition ensures that `b.recordDate` is exactly one day after `a.recordDate`.
- **Temperature Comparison**: The condition `a.temperature < b.temperature` checks for days where the temperature of `b` (the following day) is higher than `a` (the previous day).
- **Result**: The query returns the `id` of the days where the temperature was higher than the previous day.
