# 🎬 SQL Problem 1251: Average Selling Price

## 📘 Tables

### 🏷️ Prices

| Column Name | Type  |
|-------------|-------|
| product_id  | int   |
| start_date  | date  |
| end_date    | date  |
| price       | int   |

- `(product_id, start_date, end_date)` is the **primary key**.
- Each row shows the price of a product within a specific time range.
- No overlapping time ranges for the same `product_id`.

---

### 🏷️ UnitsSold

| Column Name   | Type |
|---------------|------|
| product_id    | int  |
| purchase_date | date |
| units         | int  |

- May contain **duplicate rows**.
- Each row shows a sale of some `units` of a product on a given date.

---

## 🎯 Task

Return the **average selling price** for each product, **rounded to 2 decimal places**.

- **Average Price** = Total Revenue / Total Units Sold
- If a product has **no sales**, return `0` as the average price.

---

## 📥 Example Input

### 💲 Prices

| product_id | start_date | end_date   | price |
|------------|------------|------------|-------|
| 1          | 2019-02-17 | 2019-02-28 | 5     |
| 1          | 2019-03-01 | 2019-03-22 | 20    |
| 2          | 2019-02-01 | 2019-02-20 | 15    |
| 2          | 2019-02-21 | 2019-03-31 | 30    |

### 🛒 UnitsSold

| product_id | purchase_date | units |
|------------|----------------|--------|
| 1          | 2019-02-25     | 100    |
| 1          | 2019-03-01     | 15     |
| 2          | 2019-02-10     | 200    |
| 2          | 2019-03-22     | 30     |

---

## 📤 Expected Output

| product_id | average_price |
|------------|----------------|
| 1          | 6.96           |
| 2          | 16.96          |

---

## ✅ SQL Solution

```sql
SELECT p.product_id,IFNULL(ROUND(SUM(p.price * s.units) / SUM(s.units), 2), 0) AS average_price
FROM Prices p
LEFT JOIN UnitsSold s
ON p.product_id = s.product_id
AND s.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```
---

## 📤 Explanation


- 🔗 Join Condition:

- - We join Prices and UnitsSold on the product_id

- - Also ensure purchase_date falls between start_date and end_date

- 🧮 Formula:

- - Revenue = price * units

- - Average Price = Total Revenue / Total Units

- - Use ROUND(..., 2) to keep 2 decimal places

- 🧯 Edge Case Handling:

- - Use IFNULL(..., 0) to return 0 if no sales happened for that product

---
