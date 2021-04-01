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
| UNION | UNION |
| ORDER BY | ORDER BY |

```sql
SELECT DISTINCT Movie.MovieID,
       MAX(Rating) as "Max Rating",
       AVG(Rating) as avgRating
FROM Review
WHERE role NOT IN ("admin", "premium") 
GROUP BY Movie.MovieID, Movie.Title
ORDER BY MovieID ASC, ReviewerID Desc
LIMIT 1  # only return the 1st
OFFSET 3  # omit first 3
# LIMIT和OFFSET是一种分页查询的组合
```

[对SQL执行顺序的理解](https://www.cnblogs.com/f-ck-need-u/p/8656828.html)：每一步操作都会得到一个虚拟的列表，FROM--ON--WHERE--GROUP BY--对分组的结果HAVING--WINDOW--DISTINCT--ORDER BY--TOP\(如果不排序，top随机挑选，所以基本都和order组合使用\)

## JOIN

![](../.gitbook/assets/image%20%2868%29.png)

```sql
SELECT 
# Right join means contain all data in right table
FROM A RIGHT JOIN B ON A.key = B.key 
WHERE review.rating >= 3 # review: table, rating: col
# join之后，新表中的字段仍可以用原来的表如B.col来表示，比如找出新表中NULL的row，就可以用原来表来索引，如leetcode1350
```

## Operators

<table>
  <thead>
    <tr>
      <th style="text-align:left">Operators</th>
      <th style="text-align:left">Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">LIKE<b> (wildcard matching)</b>
      </td>
      <td style="text-align:left">
        <p><b>like &#x2018;%a&#x2019;          //&#x4EE5;a&#x7ED3;&#x5C3E;&#x7684;</b>
        </p>
        <p><b>like &#x2018;%or%&#x2019;     //&#x542B;&#x6709;or&#x7684;&#x5143;&#x7D20;</b>
        </p>
        <p><b>like &#x2018;_r%&#x2019;        //&#x7B2C;&#x4E8C;&#x4F4D;&#x662F;r&#xFF0C;_&#x8868;&#x793A;&#x5355;&#x4E2A;&#x5B57;&#x7B26;</b>
        </p>
        <p><b>like &#x2018;a%o&#x2019;       //&#x4EE5;a&#x5F00;&#x5934;o&#x7ED3;&#x5C3E;&#x7684;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">REGEXP</td>
      <td style="text-align:left">
        <p>regexp &apos;a&apos; -- &#x5305;&#x542B;&#x4EFB;&#x4F55;a(A)&#x7684;</p>
        <p>regexp &apos;^a&apos; -- &#x4EE5;a(A)&#x5F00;&#x5934;&#x7684;</p>
        <p>regexp &apos;a$&apos; -- &#x4EE5;a(A)&#x7ED3;&#x5C3E;&#x7684;</p>
        <p>regexp &apos;a|b|c&apos; -- &#x5305;&#x542B;a&#x6216;b&#x6216;c</p>
        <p>regexp &apos;[gim]e&apos; --&#x5305;&#x542B;ge&#x6216;ie&#x6216;me&#x7684;</p>
        <p>regexp &apos;[a-d]e&apos; --&#x5305;&#x542B;ae&#x6216;be&#x6216;ce&#x6216;de&#x7684;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">BETWEEN</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">IN</td>
      <td style="text-align:left">&#x590D;&#x9009;&#x547D;&#x4EE4;&#xFF0C;&#x76F8;&#x5F53;&#x4E8E; where
        &#x5217; = term1 or term2 or term...</td>
    </tr>
    <tr>
      <td style="text-align:left">IS</td>
      <td style="text-align:left">WHERE Review.Rating IS NULL</td>
    </tr>
    <tr>
      <td style="text-align:left">EXISTS</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CAST</td>
      <td style="text-align:left">
        <p>CAST&#x51FD;&#x6570;&#x7528;&#x4E8E;&#x5C06;&#x67D0;&#x79CD;&#x6570;&#x636E;&#x7C7B;&#x578B;&#x7684;&#x8868;&#x8FBE;&#x5F0F;&#x663E;&#x5F0F;&#x8F6C;&#x6362;&#x4E3A;&#x53E6;&#x4E00;&#x79CD;&#x6570;&#x636E;&#x7C7B;&#x578B;&#x3002;</p>
        <p>&#x8BED;&#x6CD5;&#xFF1A;CAST (expression AS data_type)</p>
        <p>CAST(&apos;9.5&apos; AS decimal(10, 2))# &#x7CBE;&#x5EA6;&#x4E0E;&#x5C0F;&#x6570;&#x4F4D;&#x6570;&#x5206;&#x522B;&#x4E3A;10&#x4E0E;2&#x3002;&#x7CBE;&#x5EA6;&#x662F;&#x603B;&#x7684;&#x6570;&#x5B57;&#x4F4D;&#x6570;&#xFF0C;&#x5305;&#x62EC;&#x5C0F;&#x6570;&#x70B9;&#x5DE6;&#x8FB9;&#x548C;&#x53F3;&#x8FB9;&#x4F4D;&#x6570;&#x7684;&#x603B;&#x548C;&#x3002;&#x800C;&#x5C0F;&#x6570;&#x4F4D;&#x6570;&#x662F;&#x5C0F;&#x6570;&#x70B9;&#x53F3;&#x8FB9;&#x7684;&#x4F4D;&#x6570;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">%&#x53D6;&#x4F59;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x5076;&#x6570; num%2 = 0</p>
        <p>&#x5947;&#x6570; num%2 = 1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LEN()</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;&#x957F;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">substr()</td>
      <td style="text-align:left">
        <p>substr(string ,num start,num length)</p>
        <p>where lower(substr(city,1,1)) in (&apos;a&apos;,&apos;e&apos;,&apos;i&apos;,&apos;o&apos;,&apos;u&apos;);
          #&#x5F00;&#x5934;&#x5B57;&#x6BCD;&#x662F;&#x5143;&#x97F3;</p>
      </td>
    </tr>
  </tbody>
</table>

SQL的comparison operators，=, !=, &lt;, &lt;=, &gt;, &gt;=不仅可以用在numerical data，对于字符串等非数字型的数据也可以。**但是需要注意的是必须用单引号来框上该变量，SQL中用单引号来引用column中的值。**  

```sql
SELECT *
FROM table
WHERE month_name != 'January'
// can use <, > or other operators 按照字母顺序来比对
WHERE month_name > 'July'
```

## 聚合Functions

| Functions | Examples |
| :--- | :--- |
| MAX, MIN, AVG, SUM |  |
| COUNT | 聚合的计算结果虽然是一个数字，但查询的结果仍然是一个二维表，只是这个二维表只有一行一列，并且列名是`COUNT(*)。COUNT(*)`和`COUNT(id)`实际上是一样的效果。 |
|  |  |
| COUNT\(DISTINCT\) |  |

```sql
# 分组聚合
SELECT COUNT(*) num #用聚合函数后通常都会跟一个别名
FROM students
GROUP BY class_id

#return
num
4
3
4

# 按照class_id和gender分组
SELECT class_id, gender, COUNT(*) num 
FROM students 
GROUP BY class_id, gender;
```

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

It is a function that performs calculations across a set of table rows. The rows are somehow related to the current row.

窗口的概念非常重要，它可以理解为记录集合，窗口函数也就是在满足某种条件的记录集合上执行的特殊函数。对于每条记录都要在此窗口内执行函数，有的函数随着记录不同，窗口大小都是固定的，这种属于静态窗口；有的函数则相反，不同的记录对应着不同的窗口，这种动态变化的窗口叫滑动窗口。

### 基本用法

窗口函数和普通聚合函数也很容易混淆，二者区别如下：

* 聚合函数是将多条记录聚合为一条；而窗口函数是每条记录都会执行，有几条记录执行完还是几条。
* 聚合函数也可以用于窗口函数中

Example 1: 没用聚合函数，也可以实现sum，avg等功能

Typically, `OVER()` is used to compare the current row with an aggregate. For example, we can compute the difference between employee's salary and the average salary. 

over与where：需要注意的是over\(\)只计算返回的表的所有值，如果添加了where限制条件，over\(\)只计算where之后的。而且over\(\)不能放在where内，如`WHERE salary > AVG(salary) OVER ()是错的`

Example 2: calculate the difference between these two values

Example 3: 分部门计算平均工资

{% tabs %}
{% tab title="Ex1" %}
```sql
select
  first_name,
  last_name,
  salary,
  sum(salary) over()
from employee
```
{% endtab %}

{% tab title="Ex2" %}
```sql
SELECT
  first_name,
  last_name,
  salary,
  AVG(salary) OVER(),
  MAX(price) OVER() - price as difference
FROM employee;
WHERE department_id = 1
```
{% endtab %}

{% tab title="Ex3" %}
```sql
SELECT
  department_id,
  first_name,
  salary,
  AVG(salary) OVER()
FROM employee
WHERE department_id IN (1, 2, 3);
```
{% endtab %}
{% endtabs %}

### PARTITION BY

在window函数中，PARTITION BY类似于GROUP BY，如Ex1，针对每个城市求和

{% tabs %}
{% tab title="Ex1" %}
```sql
SELECT
    city,
    month,
    SUM(sold) OVER (
       PARTITION BY city
       ORDER BY month
```
{% endtab %}
{% endtabs %}

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


## 外键约束

创建外键时需要额外定义DELETE或UPDATE时该如何操作。

### 更新时相应更新CASCADE

{% embed url="https://www.youtube.com/watch?v=4JhXRll-jkQ" %}

```sql
在tag表中：
ADD CONSTRAINT `fk_tag_User`
  FOREIGN KEY (`User_id`)
  REFERENCES `User` (`id`)
  ON DELETE CASCADE
  ON UPDATE CASCADE;
```



