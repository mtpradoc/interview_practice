# Total Cost of Orders

Find the total cost of each customer's order. Output customer's id, first name, and the total order cost. Order records by customer's first name alphabetically.

customers table
id: int
first_name: varchar
last_name: varchar
city: varchar
address: varchar
phone_number: varchar

orders table
id: int
cust_id: int
order_date: datetime
order_quantity: int
order_details: varchar
order_cost: int

```sql

SELECT
  cust_id,
  first_name,
  SUM(order_cost)
FROM customer 
  JOIN orders ON customer.id = order.cust.id
GROUP BY cust_id, first_name
ORDER BY first_name ASC;

```
