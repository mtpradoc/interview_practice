# Customer Orders

Write a query to identify customers who placed more than three transactions each in both 2019 and 2020.

Input: 
transactions table
  id: integer,
  user_id: integer,
  created_at: datetime,
  product_id: integer,
  quantity: integer

users table
  id: integer,
  name: varchar

```sql
--STEP1: identify
-- transaction table - id
-- transation = customer, customer_name = name in user table
-- id from user = user_id from transactions
-- created_at in 2019/2020
  
SELECT 
  b.id as customer_id,
  b.name as customer_name
  YEAR(a.created_at) as transaction_year
  COUNT(a.id) AS transation_count
FROM transactions a
  INNER JOIN users b on a.user_id = b.id
  WHERE year(a.created_at) IN (2019, 2020)
  GROUP BY 1, 2, 3
  HAVING COUNT(a.id) > 3;

--STEP 2: Use the previous as a temporary table. Do not forget to use Distinct or group by at the end
SELECT
  DISTINCT(customer_name)
FROM
  (SELECT 
    b.id as customer_id,
    b.name as customer_name
    YEAR(a.created_at) as transaction_year
    COUNT(a.id) AS transation_count
  FROM transactions a
    INNER JOIN users b on a.user_id = b.id
    WHERE year(a.created_at) IN (2019, 2020)
    GROUP BY 1, 2, 3
    HAVING COUNT(a.id) > 3
  ) a
```
