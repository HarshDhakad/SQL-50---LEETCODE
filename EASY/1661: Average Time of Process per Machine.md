# 🏭 SQL Problem 1661: Average Time of Process per Machine

## 📘 Table: Activity

| Column Name   | Type   |
|---------------|--------|
| machine_id    | int    |
| process_id    | int    |
| activity_type | enum   |
| timestamp     | float  |

- (machine_id, process_id, activity_type) is the **primary key**.
- `activity_type` is either **'start'** or **'end'**.
- Each (machine_id, process_id) has exactly one **start** and one **end**.
- The start timestamp is **before** the end timestamp.

---

## 🎯 Task

- For each machine, calculate the **average time** taken to complete a process.
- A process time is calculated as: `end.timestamp - start.timestamp`.
- Return the `machine_id` and the **average processing time** rounded to 3 decimals.

---

## 📥 Example Input

**Activity**

| machine_id | process_id | activity_type | timestamp |
|------------|------------|----------------|-----------|
| 0          | 0          | start          | 0.712     |
| 0          | 0          | end            | 1.520     |
| 0          | 1          | start          | 3.140     |
| 0          | 1          | end            | 4.120     |
| 1          | 0          | start          | 0.550     |
| 1          | 0          | end            | 1.550     |
| 1          | 1          | start          | 0.430     |
| 1          | 1          | end            | 1.420     |
| 2          | 0          | start          | 4.100     |
| 2          | 0          | end            | 4.512     |
| 2          | 1          | start          | 2.500     |
| 2          | 1          | end            | 5.000     |

---

## 📤 Example Output

| machine_id | processing_time |
|------------|-----------------|
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |

---


## ✅ SQL Solution

```sql
SELECT a.machine_id,ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
FROM Activity aJOIN Activity b
ON a.machine_id = b.machine_id AND a.process_id = b.process_id
AND a.activity_type = 'start' AND b.activity_type = 'end'
GROUP BY a.machine_id;

```
---

## 💬 Explanation
  - We use a self join on the Activity table to pair start and end rows for the same process.

- Calculate each process time using: end.timestamp - start.timestamp.

- Use AVG() to compute the average time per machine.

- Round the result to 3 decimal places using ROUND(..., 3).

- GROUP BY ensures we get one row per machine_id.
---
