---
description: >-
  https://learnsql.com/track/sql-fundamentals/course/sql-queries/introduction/introduction/relational-databases
---

# MySQL

## General

| Syntactical Order of Operations | Logical Order of Operations |
| :--- | :--- |
| SELECT | FROM |
| DISTINCT | WHERE |
| AGGREGATIONS | GROUP BY |
| FROM | AGGREGATION |
| WHERE | HAVING |
| GROUP BY | SELECT |
| HAVING | DISTINCT |
| ORDER BY | ORDER BY |

```sql
SELECT DISTINCT Movie.MovieID,
       MAX(Rating) as maxRating,
       AVG(Rating) as avgRating
FROM Review
WHERE role NOT IN ("admin", "premium") 
GROUP BY Movie.MovieID, Movie.Title
ORDER BY MovieID ASC, ReviewerID Desc
LIMIT 1  # only return the 1st
OFFSET 3  # omit first 3
```

## JOIN

![](../.gitbook/assets/image%20%2868%29.png)

```sql
SELECT 
# Right join means contain all data in right table
FROM A RIGHT JOIN B ON A.key = B.key 
WHERE review.rating >= 3 # review: table, rating: col
```

## Operators

| Operators | Examples |
| :--- | :--- |
| LIKE **\(wildcard matching\)** |  |
| BETWEEN |  |
| IN |  |
| IS | WHERE Review.Rating IS NULL |
| EXISTS |  |

## Functions

| Functions | Examples |
| :--- | :--- |
| MAX, MIN, AVG, SUM |  |
| COUNT |  |
| COUNT\(DISTINCT\) |  |

## WHERE & HAVING

**Having** clause acts as a filter on aggregated data. In other words, this is the way that you filter on the results of your aggregate functions.

```sql
SELECT Movie.MovieID,
       Movie.Title,
       MAX(Rating) as maxRating,
       AVG(Rating) as avgRating
FROM   Movie 
INNER JOIN Review 
   ON Movie.MovieID = Review.MovieID
GROUP BY Movie.MovieID, Movie.Title
HAVING AVG(Rating) < 3
```

## [Window Function](https://learnsql.com/blog/sql-window-functions-cheat-sheet/Window_Functions_Cheat_Sheet.pdf)

窗口的概念非常重要，它可以理解为记录集合，窗口函数也就是在满足某种条件的记录集合上执行的特殊函数。对于每条记录都要在此窗口内执行函数，有的函数随着记录不同，窗口大小都是固定的，这种属于静态窗口；有的函数则相反，不同的记录对应着不同的窗口，这种动态变化的窗口叫滑动窗口。

窗口函数和普通聚合函数也很容易混淆，二者区别如下：

* 聚合函数是将多条记录聚合为一条；而窗口函数是每条记录都会执行，有几条记录执行完还是几条。
* 聚合函数也可以用于窗口函数中

```sql
table
+----+-------+--------+--------------+
| Id | Name  | Salary | Department |     
+----+-------+--------+--------------+
| 1  | Joe   | 85000  | IT            |      
| 2  | Henry | 80000  | SALES     |
| 3  | Sam   | 60000  | SALES      |
| 4  | Max   | 90000  | IT            |
| 5  | Janet | 69000  | IT            |
| 6  | Randy | 85000  | IT            |
| 7  | Will  | 70000  | IT            |
+----+-------+--------+--------------+


TOP 3 Salary within each department

\+------------+----------+--------+
| Department | Name| Salary | 
+------------+----------+--------+
| IT         | Max      | 90000  |      
| IT         | Randy    | 85000  |    
| IT         | Joe      | 85000  |    
| IT         | Will     | 70000  |      
| Sales      | Henry    | 80000   | 
| Sales      | Sam      | 60000  |  
+------------+----------+--------+


SELECT department, name, salary from
(
SELECT *, DENSE_RANK() OVER (PARTITION BY Department ORDER BY Salary) AS rank
FROM table
WHERE rank <= 3
);


Window Function






table
+--------------+-------------+------------+
| requester_id | accepter_id | accept_date|
|--------------|-------------|------------|
| 1            | 2           | 2016_06-03 |
| 1            | 3           | 2016-06-08 |
| 2            | 3           | 2016-06-08 |
| 3            | 4           | 2016-06-09 |
+--------------+-------------+------------+

Write a query to find the people who has most friends.

+------+------+
| id   | num  |
|------|------|
| 3    | 3    |
+------+------+



SELECT id, count(id) AS num 
FROM
(
SELECT requested_id id from table
UNION ALL
SELECT accepted_id id from table
)
GROUP BY ID
ORDER BY num DESC
LIMIT 1;













Given a Weather table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.
+---------+------------------+------------------+
| Id(INT) | RecordDate(DATE) | Temperature(INT) |
+---------+------------------+------------------+
|       1 |       2015-01-01 |               10 |
|       2 |       2015-01-02 |               25 |
|       3 |       2015-01-03 |               20 |
|       4 |       2015-01-04 |               30 |
+---------+------------------+------------------+

For example, return the following Ids for the above Weather table:
+----+
| Id |
+----+
|  2 |
|  4 |
+----+

SELECT a.Id AS Id
FROM table a
JOIN table b 
ON DATEDIFF(a.RecordDate, b.RecordDate) = 1
AND a.Temperature > b.Temperature;

SELECT a.Id AS Id
from table a, table b
WHERE DATEDIFF(a.RecordDate, b.RecordDate) = 1
AND a.Temperature > b.Temperature

Self Join

```

[https://stevestedman.com/2013/04/rows-and-range-preceding-and-following/](https://stevestedman.com/2013/04/rows-and-range-preceding-and-following/)  




