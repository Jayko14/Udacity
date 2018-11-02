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

## Chapter 3, Lesson 17
Q1)
SELECT a.name, AVG(o.standard_qty) average_standard, AVG(o.gloss_qty) average_gloss, AVG(o.poster_qty) average_poster
FROM orders o
JOIN accounts a
ON a.id = o.id
GROUP BY a.name;
Q2)
SELECT a.name, AVG(o.standard_amt_usd) average_standard, AVG(o.gloss_amt_usd) average_gloss, AVG(o.poster_amt_usd) average_poster
FROM orders o
JOIN accounts a
ON a.id = o.id
GROUP BY a.name;
Q3)
SELECT w.channel, s.name, COUNT(*) occ
FROM sales_reps s
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN web_events w 
ON w.account_id = a.id
GROUP BY w.channel, s.name
ORDER BY occ DESC;
Q4)
SELECT w.channel, r.name region, COUNT(*) occ
FROM sales_reps s
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN web_events w 
ON w.account_id = a.id
JOIN region r
ON r.id = s.region_id
GROUP BY w.channel, r.name
ORDER BY occ DESC;

## Chapter 3, Lesson 23
Q1) 
SELECT s.name sales, COUNT(*) mng
FROM accounts a
JOIN sales_reps s
ON s.id = a.sales_rep_id
GROUP BY s.name
HAVING COUNT(*) >5
ORDER BY COUNT(*)
Q2)
SELECT account_id, COUNT(*)
FROM orders
GROUP BY account_id
HAVING COUNT(*) > 20;
Q3)
SELECT o.account_id, a.name, COUNT(*)
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY o.account_id, a.name
HAVING COUNT(*) > 20
ORDER BY COUNT(*) DESC;
Q4)
SELECT o.total_amt_usd, a.name
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY a.name, o.total_amt_usd
HAVING o.total_amt_usd > 30000;
Q5)
SELECT o.total_amt_usd, a.name
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY a.name, o.total_amt_usd
HAVING o.total_amt_usd < 1000;
Q6)
SELECT sum(o.total_amt_usd), a.name
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY a.name
ORDER BY sum(o.total_amt_usd) DESC; 
Q7)
SELECT sum(o.total_amt_usd), a.name
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY a.name
ORDER BY sum(o.total_amt_usd); 
Q8)
SELECT a.name, w.channel, COUNT(*) AS contact
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.name, w.channel
HAVING w.channel = 'facebook' AND COUNT(*) >6;
Q9)
SELECT a.name, w.channel, COUNT(*) AS contact
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.name, w.channel
HAVING w.channel = 'facebook' AND COUNT(*) >6
ORDER BY COUNT(*) DESC;
Q10)
SELECT a.name, w.channel, COUNT(w.channel) AS times
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.name, w.channel
ORDER BY COUNT(w.channel) DESC;

##Chapter 3, Lesson 31
Q1) 
SELECT a.name, SUM(total_amt_usd) total_spent,	 
	CASE WHEN SUM(total_amt_usd) > 200000 THEN 'Top' 
	WHEN SUM(total_amt_usd) < 200000 AND SUM(total_amt_usd) > 100000 THEN 'Middle' 
	ELSE 'Low' END AS Membership
FROM orders o
JOIN accounts a
ON o.account_id = a.id
GROUP BY a.name
ORDER BY total_spent DESC;
Q2)
SELECT a.name, SUM(total_amt_usd) total_spent, 	 
	CASE WHEN SUM(total_amt_usd) > 200000 THEN 'Top' 
	WHEN SUM(total_amt_usd) < 200000 AND SUM(total_amt_usd) > 100000 THEN 'Middle' 
	ELSE 'Low' END AS Membership
FROM orders o
JOIN accounts a
ON o.account_id = a.id
WHERE o.occurred_at > '2015-12-31'
GROUP BY a.name
ORDER BY total_spent DESC;
Q3)
SELECT s.name rep_name, count(*), CASE WHEN count(*) > 200 THEN 'top' ELSE 'not' END AS sales_rep_tier
FROM sales_reps s
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN orders o
ON a.id = o.account_id
GROUP BY s.name
ORDER BY 2 DESC;
Q4)
SELECT s.name rep_name, SUM(o.total_amt_usd), count(*), CASE WHEN count(*) > 200 OR sum(o.total_amt_usd) > 750000 THEN 'top' WHEN count(*) > 150 OR SUM(o.total_amt_usd) > 500000 THEN 'mid' ELSE 'low' END AS sales_rep_tier
FROM sales_reps s
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN orders o
ON a.id = o.account_id
GROUP BY s.name
ORDER BY 2 DESC;

#Chapter 4 
##Chapter 4, Lesson 10
Q1) 
SELECT t3.rep_name , t2.region, t2.max 
FROM(
SELECT region, MAX(total_amt) max
FROM (
SELECT s.name rep_name, r.name region, SUM(o.total_amt_usd) total_amt                     
FROM region r
JOIN sales_reps s
ON r.id = s.region_id
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN orders o
ON a.id = o.account_id
GROUP BY 1,2) t1
GROUP BY 1) t2
JOIN (
  SELECT s.name rep_name, r.name region, SUM(o.total_amt_usd) total_amt                     
FROM region r
JOIN sales_reps s
ON r.id = s.region_id
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN orders o
ON a.id = o.account_id
GROUP BY 1,2) t3
ON t2.region = t3.region AND t2.max = t3.total_amt
ORDER BY max DESC;
Q2)
SELECT region, SUM(total_amt), COUNT(cnt)
FROM(
SELECT r.name region, (o.total_amt_usd) total_amt, o.total cnt
FROM region r
JOIN sales_reps s
ON r.id = s.region_id
JOIN accounts a
ON s.id = a.sales_rep_id
JOIN orders o
ON a.id = o.account_id) t1
GROUP BY 1
ORDER BY 2 DESC;
Q3)
SELECT COUNT(*)
FROM(
SELECT a.name
FROM orders o
JOIN accounts a
ON a.id = o.account_id
GROUP BY 1
HAVING SUM(o.total) > (SELECT t1.std_qty
FROM(
SELECT a.name accounts, SUM(o.standard_qty) std_qty, SUM(o.total) total
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1) t1))t2
Q4)
SELECT a.name account, w.channel,COUNT(w.channel) count
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY 1,2
HAVING a.name = (
SELECT t1.account
FROM(
SELECT a.name account, SUM(o.total_amt_usd) total
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1) t1)
Q5)
SELECT t1.account, t1.total/ (t1.max-t1.min) avg
FROM(
SELECT a.name account, SUM(o.total_amt_usd) total, MAX(DATE_PART('year',occurred_at)) max,
MIN(DATE_PART('year', occurred_at)) min
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY 1
ORDER BY total DESC
LIMIT 10) t1;
Q6)
SELECT t1.account, AVG(t1.total)
FROM (
SELECT a.name account, SUM(o.total_amt_usd) total
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY 1
ORDER BY 2 DESC) t1
GROUP BY 1
HAVING AVG(t1.total) > (SELECT AVG(total)
FROM
(SELECT a.name account, SUM(o.total_amt_usd) total
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY 1
ORDER BY 2 DESC)t2)
