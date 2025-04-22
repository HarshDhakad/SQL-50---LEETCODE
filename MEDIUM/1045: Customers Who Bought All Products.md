# 🛒 SQL Problem 1045: Customers Who Bought All Products

## 📘 Table: Customer

| Column Name | Type |
|-------------|------|
| customer_id | int  |
| product_key | int  |

- May contain **duplicate rows**.
- `customer_id` is **not NULL**.
- `product_key` is a **foreign key** referencing the `Product` table.

---

## 📘 Table: Product

| Column Name | Type |
|-------------|------|
| product_key | int  |

- `product_key` is the **primary key**.

---

## 🎯 Task

Find the `customer_id`s who bought **all products** from the `Product` table.

---

## 📥 Example Input
### Customer

| customer_id | product_key |
|-------------|-------------|
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |

### Product

| product_key |
|-------------|
| 5           |
| 6           |

---

## 📤 Expected Output

| customer_id |
|-------------|
| 1           |
| 3           |

---

## ✅ SQL Solution

```sql
SELECT customer_id FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT(product_key))=(SELECT COUNT(DISTINCT product_key) FROM Product)
```
