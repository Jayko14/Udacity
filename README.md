# Chapter 1
## Chapter 1, Lesson 19
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

## Chapter 1, Lesson 25
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

## Chapter 1, Lesson 28
Q1) 
SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';

## Chapter 1, Lesson 31
Q1)
SELECT standard_amt_usd/standard_qty AS standard_cost, id, account_id
FROM orders
LIMIT 10
Q2)
SELECT id, account_id, (gloss_amt_usd/total_amt_usd)*100 AS pct_rvu
FROM orders

## Chapter 1, Lesson 35
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

## Chapter 1, Lesson 38
Q1)
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom');
Q2)
SELECT * 
FROM web_events
WHERE channel IN ('organic', 'adwords');

## Chapter 1, Lesson 41
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

## Chapter 1, Lesson 44
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

## Chapter 1, Lesson 47
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
 
# Chapter 2
## Chapter 2, Lesson 12
Q1)
SELECT a.name, a.primary_poc, w.occurred_at, w.channel
FROM web_events w
JOIN accounts a
ON w.account_id = a.id 
WHERE name = 'Walmart';
Q2)
SELECT acc.name, acc.sales_rep_id, sal.region_id
FROM accounts acc
JOIN sales_reps sal
ON acc.sales_rep_id = sal.id
ORDER BY acc.name;
Q3)
SELECT reg.name as region, acc.name, (ord.total_amt_usd/(ord.total+0.01)) AS unit_price
FROM accounts acc
JOIN sales_reps sal
ON acc.sales_rep_id = sal.id
JOIN orders ord
ON acc.id = ord.account_id
JOIN region reg

## Chapter 2, Final boss
Q1)
SELECT a.name, s.name as sales, r.name as region
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
WHERE r.name = 'Midwest'
ORDER BY a.name 
Q2)
SELECT a.name, s.name as sales, r.name as region
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r 
ON s.region_id = r.id
WHERE r.name = 'Midwest' AND s.name LIKE 'S%'
ORDER BY a.name 
Q3)
SELECT a.name, s.name as sales, r.name as region
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r 
ON s.region_id = r.id
WHERE r.name = 'Midwest' AND s.name LIKE '% K%'
ORDER BY a.name 
Q4)
SELECT r.name as region, a.name, (o.total_amt_usd/(o.total+0.01)) unit_price
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty >100;
Q5)
SELECT r.name as region, a.name, (o.total_amt_usd/(o.total+0.01)) unit_price
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty >100 AND o.poster_qty >50
ORDER BY unit_price;
Q6)
SELECT r.name as region, a.name, (o.total_amt_usd/(o.total+0.01)) unit_price
FROM accounts a
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty >100 AND o.poster_qty >50
ORDER BY unit_price DESC;
Q7)
SELECT DISTINCT a.name, w.channel
FROM accounts a
JOIN web_events w
ON w.account_id = a.id
WHERE a.id = 1001;
Q8)
SELECT a.name, o.occurred_at, o.total, o.total_amt_usd
FROM accounts a
JOIN orders o
ON o.account_id = a.id
where o.occurred_at BETWEEN '2015-01-01' AND '2016-01-01';

## Chapter 3, lesson 14
Q1) 
SELECT a.name, o.occurred_at 
FROM orders o
JOIN accounts a
ON o.id = a.id
ORDER BY o.occurred_at;
Q2)
SELECT a.name, SUM(o.total_amt_usd)
FROM orders o
JOIN accounts a
ON o.id = a.id
GROUP BY a.name;
Q3)
SELECT a.name, o.occurred_at AS OCC, w.channel, w.occurred_at
FROM orders o
JOIN accounts a
ON o.id = a.id
JOIN web_events w
ON o.id = w.id
ORDER BY w.occurred_at DESC;
Q4) 
SELECT channel, COUNT(channel)
FROM web_events
GROUP BY channel;
Q5)
SELECT a.primary_poc, w.occurred_at
FROM accounts a
JOIN web_events w
ON w.id = a.id
ORDER BY occurred_at;
Q6)
SELECT a.name, o.total_amt_usd
FROM accounts a
JOIN orders o
ON o.id = a.id
GROUP BY a.name
ORDER BY total_amt_usd;
Q7)
SELECT COUNT(s.name), r.name AS region
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
GROUP BY region
ORDER BY count;

