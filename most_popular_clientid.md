# The Most Popular Clien_id Among Users Using Video and Voice Calls

Select the most popular client_id based on a count of the number of users who have at least 50% of their events from the following 
list: 'video call received', 'video call sent', 'voice call received', 'voice call sent'

fact_events

id: int,
time_id: datetime,
user_id: varchar,
customer_id: varchar,
client_id: varchar,
event_type: varchar,
event_id: int

```sql

-- users who have at least 50% of their events being call events
-- count these user per client_di
-- limit output to 1 client_id (most users)

--STEP 1: Identify the 'who have at least 50%'
SELECT
  user_id,
  AVG(CASE
    WHEN event_type IN ('video call received', 'video call sent', 'voice call received', 'voice call sent')
    THEN 1 ELSE 0 END)
FROM fact_events
GROUP BY 1
HAVING AVG(CASE
    WHEN event_type IN ('video call received', 'video call sent', 'voice call received', 'voice call sent')
    THEN 1 ELSE 0 END) >= 0.5;

--STEP 2: Identify the client_id and user_id that comply with the requirements
SELECT
  client_id,
  user_id
FROM fact_events
GROUP BY 1,2
HAVING AVG(CASE
    WHEN event_type IN ('video call received', 'video call sent', 'voice call received', 'voice call sent')
    THEN 1 ELSE 0 END) >= 0.5;

--STEP 3: Use the previous table as a temp table
SELECT
  client_id,
  COUNT(user_id)
FROM
    (SELECT
      client_id,
      user_id
    FROM fact_events
    GROUP BY 1,2
    HAVING AVG(CASE
        WHEN event_type IN ('video call received', 'video call sent', 'voice call received', 'voice call sent')
        THEN 1 ELSE 0 END) >= 0.5)  call_users
GROUP BY 1
ORDER BY   COUNT(user_id) DESC
LIMIT 1

--STEP 3: Remove the COUNT
SELECT
  client_id
FROM
    (SELECT
      client_id,
      user_id
    FROM fact_events
    GROUP BY 1,2
    HAVING AVG(CASE
        WHEN event_type IN ('video call received', 'video call sent', 'voice call received', 'voice call sent')
        THEN 1 ELSE 0 END) >= 0.5)  call_users
GROUP BY 1
ORDER BY   COUNT(user_id) DESC
LIMIT 1

```
