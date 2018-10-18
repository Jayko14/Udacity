# Udacity
#Chapter 1, Lesson 19
Q1) 
SELECT id, occurred_at, total_amt_usd FROM orders
ORDER BY occurred_at 
LIMIT 10
Q2)
SELECT id, account_id, total_amt_usd FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5
Q3)
SELECT id, account_id, total
FROM orders
ORDER BY total
LIMIT 20

## Chapter 1, Lesson 22
Q1)
SELECT total_amt_usd, occurred_at 
FROM orders
ORDER BY occurred_at DESC, total_amt_usd
LIMIT 5
Q2) 
SELECT total_amt_usd, occurred_at
FROM orders
ORDER BY occurred_at, total_amt_usd
Limit 10

### Chapter 1, Lesson 25
Q1) 
SELECT * 
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
Q2)
SELECT * 
FROM orders
WHERE total_amt_usd < 500
LIMIT 10;

#### Chapter 1, Lesson 28
Q1) 
SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';

##### Chapter 1, Lesson 31
Q1)
SELECT standard_amt_usd/standard_qty AS standard_cost, id, account_id
FROM orders
LIMIT 10
Q2)
SELECT id, account_id, (gloss_amt_usd/total_amt_usd)*100 AS pct_rvu
FROM orders

###### Chapter 1, Lesson 35
Q1) 
SELECT * 
FROM accounts
WHERE name LIKE 'C%';
Q2)
SELECT * 
FROM accounts
WHERE name LIKE '%one%';
Q3)
SELECT * 
FROM accounts
WHERE name LIKE '%s';

########## Chapter 1, Lesson 38
Q1)
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom');
Q2)
SELECT * 
FROM web_events
WHERE channel IN ('organic', 'adwords');

###### Chapter 1, Lesson 41
Q1)
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name NOT IN ('Walmart', 'Target', 'Nordstrom');
Q2)
SELECT * 
FROM web_events
WHERE channel NOT IN ('organic', 'adwords');
Q3)
Select * 
FROM accounts
WHERE name NOT LIKE 'C%';
Q4)
SELECT * 
FROM accounts
WHERE name NOT LIKE '%one%';
Q5)
SELECT * 
FROM accounts
WHERE name NOT LIKE '%s';

#### Chapter 1, Lesson 44
Q1)
SELECT *
FROM orders
WHERE standard_qty>1000 AND poster_qty=0 AND gloss_qty=0;
Q2)
SELECT name 
FROM accounts
WHERE name NOT LIKE 'C%' AND name NOT LIKE '%s';
Q3)
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;

###### Chapter 1, Lesson 47
Q1)
SELECT id
FROM orders
WHERE gloss_qty>4000 OR poster_qty>4000;
Q2)
SELECT * 
FROM orders
WHERE standard_qty = 0 AND (gloss_qty >1000 OR poster_qty >1000);
Q3)
SELECT name, primary_poc
FROM accounts
WHERE (name LIKE 'C%' OR name LIKE 'W%') AND (primary_poc LIKE '%ana%' OR primary_poc LIKE'Ana%') AND (primary_poc NOT LIKE '%eana%');






