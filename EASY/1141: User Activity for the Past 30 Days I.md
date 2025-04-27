# 👤 LeetCode SQL Problem 1141: User Activity for the Past 30 Days I

## 🧾 Table: Activity

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| session_id    | int     |
| activity_date | date    |
| activity_type | enum    |

- This table **may have duplicate rows**.
- `activity_type` is an ENUM: ('open_session', 'end_session', 'scroll_down', 'send_message').
- Each session belongs to exactly **one user**.

---

### ℹ️ Notes:
- Find the **daily active user count** for the **30-day period ending 2019-07-27** (inclusive).
- A **user is considered active** on a day if they did **at least one activity**.
- Do **not show days with zero active users**.

---

## 🎯 Task

Write a solution to **count the number of active users per day** within the specified 30-day period.

---

## 📥 Example Input

### Activity Table

| user_id | session_id | activity_date | activity_type |
|---------|------------|---------------|---------------|
| 1       | 1          | 2019-07-20     | open_session  |
| 1       | 1          | 2019-07-20     | scroll_down   |
| 1       | 1          | 2019-07-20     | end_session   |
| 2       | 4          | 2019-07-20     | open_session  |
| 2       | 4          | 2019-07-21     | send_message  |
| 2       | 4          | 2019-07-21     | end_session   |
| 3       | 2          | 2019-07-21     | open_session  |
| 3       | 2          | 2019-07-21     | send_message  |
| 3       | 2          | 2019-07-21     | end_session   |
| 4       | 3          | 2019-06-25     | open_session  |
| 4       | 3          | 2019-06-25     | end_session   |

---

## 📤 Expected Output

| day        | active_users |
|------------|--------------|
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |

---

### 🧠 Explanation:
- **2019-07-20**: Users 1 and 2 were active.
- **2019-07-21**: Users 2 and 3 were active.
- Ignore 2019-06-25 because it is **outside the 30-day window**.

---

## ✅ SQL Solution
## Method 1
```sql
SELECT activity_date as day,COUNT(DISTINCT(user_id)) as active_users FROM Activity
WHERE activity_date<='2019-07-27' AND DATEDIFF('2019-07-27',activity_date)<30
GROUP BY activity_date
```
## Method 2
```sql
SELECT activity_date as day,COUNT(DISTINCT(user_id)) as active_users FROM Activity
WHERE activity_date BETWEEN DATE_SUB('2019-07-27',INTERVAL 29 DAY) AND '2019-07-27'
GROUP BY activity_date
```

---
## TIPS->
- BETWEEN takes two arguments separated by AND and includes both the start and end dates.

- DATE_SUB(date, INTERVAL n DAY) is used to subtract a number of days from a given date.

- Here, by using INTERVAL 29 DAY, we are finding the date that is 29 days before '2019-07-27'.
- Thus, the range covers 30 days in total (from '2019-06-28' to '2019-07-27' inclusive). 
---
