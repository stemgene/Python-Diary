---
description: >-
  https://learnsql.com/track/sql-fundamentals/course/sql-queries/introduction/introduction/relational-databases
---

# MySQL

## General

| Syntactical Order of Operations | Logical Order of Operations |
| ------------------------------- | --------------------------- |
| SELECT                          | FROM                        |
| DISTINCT                        | WHERE                       |
| AGGREGATIONS                    | GROUP BY                    |
| FROM                            | AGGREGATION                 |
| WHERE                           | HAVING                      |
| GROUP BY                        | SELECT                      |
| HAVING                          | DISTINCT                    |
| UNION                           | UNION                       |
| ORDER BY                        | ORDER BY                    |
| LIMIT                           |                             |

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

[对SQL执行顺序的理解](https://www.cnblogs.com/f-ck-need-u/p/8656828.html)：每一步操作都会得到一个虚拟的列表，FROM--ON--WHERE--GROUP BY--对分组的结果HAVING--WINDOW--DISTINCT--ORDER BY--TOP(如果不排序，top随机挑选，所以基本都和order组合使用)

## Operators

| Operators                              | Examples                                                                                                                                                                                                             |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LIKE **** (wildcard matching)          | <p>like ‘%a’          //以a结尾的</p><p>like ‘%or%’     //含有or的元素</p><p>like ‘_r%’        //第二位是r，_表示单个字符</p><p>like ‘a%o’       //以a开头o结尾的</p>                                                                          |
| REGEXP                                 | <p>regexp 'a'       -- 包含任何a(A)的</p><p>regexp '^a'     -- 以a(A)开头的</p><p>regexp 'a$'    -- 以a(A)结尾的</p><p>regexp 'a|b|c' -- 包含a或b或c</p><p>regexp '[gim]e'  --包含ge或ie或me的</p><p>regexp '[a-d]e'  --包含ae或be或ce或de的</p> |
| BETWEEN                                | <p>SELECT name, area </p><p>FROM world </p><p>WHERE area BETWEEN 250 AND 3000</p>                                                                                                                                    |
| IN                                     | 复选命令，相当于 where 列 = term1 or term2 or term...                                                                                                                                                                         |
| IS                                     | WHERE Review.Rating IS NULL                                                                                                                                                                                          |
|                                        | <p>ORDER BY state DESC, first_name ASEC  --先按照state排序，如果state一致再按name排</p><p>即使SELETE没选中排序的列，也仍然可以按照该列排序，select birthday order by name</p>                                                                           |
| EXISTS                                 |                                                                                                                                                                                                                      |
| CAST                                   | <p>CAST函数用于将某种数据类型的表达式显式转换为另一种数据类型。</p><p>语法：CAST (expression AS data_type)</p><p>CAST('9.5' AS decimal(10, 2))# 精度与小数位数分别为10与2。精度是总的数字位数，包括小数点左边和右边位数的总和。而小数位数是小数点右边的位数</p>                                         |
| %取余数                                   | <p>偶数 num%2 = 0</p><p>奇数 num%2 = 1</p>                                                                                                                                                                               |
| LEN()                                  | 字符串长度                                                                                                                                                                                                                |
| substr()                               | <p>substr(string ,num start,num length)</p><p>where lower(substr(city,1,1)) in ('a','e','i','o','u'); #开头字母是元音</p>                                                                                                   |
| FIRST_VALUE() / LAST_VALUE()           |                                                                                                                                                                                                                      |
| LAG()                                  |                                                                                                                                                                                                                      |
| LEAD()                                 |                                                                                                                                                                                                                      |
| RANK() / DENSE_RANK() / PERCENT\_RANK_ |                                                                                                                                                                                                                      |
| CUME\_DIST()                           |                                                                                                                                                                                                                      |
| NTILE()                                |                                                                                                                                                                                                                      |
| ROW\_NUMBER()                          |                                                                                                                                                                                                                      |
| date\_diff(日期1, 日期2)                   | <p>日期1与日期2相差的天数。 </p><p>如果日期1比日期2大，结果为正；</p><p>如果日期1比日期2小，结果为负。</p>                                                                                                                                                  |
| timestampdiff(时间类型, 日期1, 日期2)          | <p>“时间类型”的参数，“day”, “hour”, “second”等<br>日期1大于日期2，结果为负，日期1小于日期2，结果为正。</p>                                                                                                                                            |
| YEAR()                                 | WHERE YEAR(birth\_date) = 2010;                                                                                                                                                                                      |

SQL的comparison operators，=, !=, <, <=, >, >=不仅可以用在numerical data，对于字符串等非数字型的数据也可以。**但是需要注意的是必须用单引号来框上该变量，SQL中用单引号来引用column中的值。** &#x20;

```sql
SELECT *
FROM table
WHERE month_name != 'January'
// can use <, > or other operators 按照字母顺序来比对
WHERE month_name > 'July'
```

## IF and SWITCH

### IF 和JAVA一样是三段论

```sql
IF (MOD(employee_id, 2) = 1 AND name NOT LIKE 'M%', salary, 0) as bonus

UPDATE Salary SET sex = IF (sex = 'm', 'f', 'm');
```

### CASE

```sql
CASE WHEN MOD(employee_id,2) = 1 THEN salary,
     ELSE 0 
END as bonus
```

## JOIN

### JOIN两个表

默认的JOIN表达式就是inner join。而LEFT JOIN，RIGHT JOIN和FULL OUTER JOIN都是outer join

![](<../../.gitbook/assets/image (68).png>)

```sql
SELECT 
# Right join means contain all data in right table
FROM A 
RIGHT JOIN B 
    ON A.key = B.key 
    或 using (key) 当两个表的字段名一致时，可以使用using (）使语句更简单
WHERE review.rating >= 3 # review: table, rating: col
# join之后，新表中的字段仍可以用原来的表如B.col来表示，比如找出新表中NULL的row，就可以用原来表来索引，如leetcode1350
```

### JOIN多个表

![多个表的inner join](<../../.gitbook/assets/image (105).png>)

![多个表的outer join](<../../.gitbook/assets/image (93).png>)

### SELF JOIN

self join的目的是让表中同一列的值出现在两列中。比如下方例子中的first name，既要当员工，也要当manager。再如汽车站stop，既要当出发点，也要当目的地。此时就把表定义成a和b，然后join

![表自身的inner join](<../../.gitbook/assets/image (101).png>)

![](<../../.gitbook/assets/image (95).png>)

上面的表自身的join返回的结果其实是缺了CEO自己的，因为CEO对应的manager是NULL，所以此时应该用outer join来返回所有的员工

![](<../../.gitbook/assets/image (102).png>)

![](<../../.gitbook/assets/image (96).png>)

### Compound Join Conditions一表中多个primary key的JOIN操作

需要JOIN table2 ON t1.term1 = t2.term1 AND ON t1.term2 = t2.term2

![](<../../.gitbook/assets/image (98).png>)

由于上面两个表中的字段名都是一样的，可以用using简化query语句

```sql
SELECT *
FROM order_items oi
JOIN order_item_notes oin
    using (order_id, product_id)
```

### Implicit Join

以下两个表达式所查询出的结果是一样的，但利用implicit join一旦忘了加入where，就是两个表的outter join，会造成系统负载过大

![](<../../.gitbook/assets/image (99).png>)

## UNION 组合多个query需求，将一张表或多张表按照条件连接到一起

* 组合多个query需求，在同一个结果中返回
* 每一个单独的query返回的格式需相同
* 可以在一张表内，或者多张表联合使用
* 多张表时，column的title是第一个query的标题

### 单张表

想要把下表按照日期分类，2019年以后的为active，2019年以前的为archive

```sql
SELECT 
  order_id,
  order_date,
  'Active' as 'Status'   -- 这一列是新加的纯文本列
FROM orders
WHERE order_date >= '2019'
UNION
SELECT 
  order_id,
  order_date,
  'Archived' as 'Status'
FROM orders
WHERE order_date < '2019'
```

![](<../../.gitbook/assets/image (109).png>)

### 多张表

![](<../../.gitbook/assets/image (103).png>)

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

## [Window Function](https://learnsql.com/blog/sql-window-functions-cheat-sheet/Window\_Functions\_Cheat\_Sheet.pdf)

It is a function that performs calculations across a set of table rows. The rows are somehow related to the current row.

窗口的概念非常重要，它可以理解为记录集合，窗口函数也就是在满足某种条件的记录集合上执行的特殊函数。对于每条记录都要在此窗口内执行函数，有的函数随着记录不同，窗口大小都是固定的，这种属于静态窗口；有的函数则相反，不同的记录对应着不同的窗口，这种动态变化的窗口叫滑动窗口。

### 基本用法

窗口函数和普通聚合函数也很容易混淆，二者区别如下：

* 聚合函数是将多条记录聚合为一条；而窗口函数是每条记录都会执行，有几条记录执行完还是几条。
* 聚合函数也可以用于窗口函数中

Example 1: 没用聚合函数，也可以实现sum，avg等功能

Typically, `OVER()` is used to compare the current row with an aggregate. For example, we can compute the difference between employee's salary and the average salary.&#x20;

over与where：需要注意的是over()只计算返回的表的所有值，如果添加了where限制条件，over()只计算where之后的。而且over()不能放在where内，如`WHERE salary > AVG(salary) OVER ()是错的`

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

[https://stevestedman.com/2013/04/rows-and-range-preceding-and-following/](https://stevestedman.com/2013/04/rows-and-range-preceding-and-following/)\


## 表与表之间的关系

### Many to Many

如果两个表的关系是Many-to-Many，如students对应teachers，需要中间一个表保存对应关系

![中间的表保存对应关系](<../../.gitbook/assets/image (104).png>)

Query查询的时候，可以从左向右依次查，如先JOIN students和students\_teachers on `student_id`，然后再JOIN students\_teachers和teachers on `teacher_id`。





![](<../../.gitbook/assets/image (100).png>)

## 外键约束&#x20;

{% embed url="https://dev.mysql.com/doc/refman/8.0/en/create-table-foreign-keys.html" %}

创建外键时需要额外定义DELETE或UPDATE时该如何操作。要明确parent和child的关系，带REFERENCE的是parent，如果parent删除，child要跟着删除。但反过来则没有限制。对于UPDATE，可以参考category对应着variable，如果category表的id变化从2变为3，那variable表中的category也统一变为3

TIPs：

* 通过Workbench创建sql时，有可能不成功。因为Workbench默认情况下会执行safe策略，即不执行关联删除等容易把数据清空的操作，此时可以在设置中更改。
* 当调试时需要删除某表但因为FK约束而报错。此时可以临时取消所有FK的限制`SET foreign_key_checks = 0;`然后就可以正常删除了，当然删除后别忘了再改回1。

### 更新时相应更新CASCADE

{% embed url="https://www.youtube.com/watch?v=4JhXRll-jkQ" %}

外键并不是通过列名实现的，而是通过定义外键约束实现的：

```sql
CREATE TABLE parent (
    id INT NOT NULL,
    PRIMARY KEY (id)
) ENGINE=INNODB;

CREATE TABLE child (
    id INT,
    parent_id INT,
    INDEX par_ind (parent_id),
    FOREIGN KEY (parent_id)
        REFERENCES parent(id) -- 上一级，如果parent表删除，此表跟着删除
        ON DELETE CASCADE
) ENGINE=INNODB;

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT

```

下面的表就比较复杂，`product_order`有两个FK对应着两张表，一个对应着只有两列index的`product`表。另一个对应着单行index的`customer`表

```sql
CREATE TABLE customer (
    id INT NOT NULL,
    PRIMARY KEY (id)
)   ENGINE=INNODB;

CREATE TABLE product (
    category INT NOT NULL, id INT NOT NULL,
    price DECIMAL,
    PRIMARY KEY(category, id)
)   ENGINE=INNODB;

CREATE TABLE product_order (
    no INT NOT NULL AUTO_INCREMENT,
    product_category INT NOT NULL,
    product_id INT NOT NULL,
    customer_id INT NOT NULL,

    PRIMARY KEY(no),
    INDEX (product_category, product_id),
    INDEX (customer_id),

    FOREIGN KEY (product_category, product_id)
      REFERENCES product(category, id)
      ON UPDATE CASCADE ON DELETE RESTRICT,

    FOREIGN KEY (customer_id)
      REFERENCES customer(id)
)   ENGINE=INNODB;
```

![](<../../.gitbook/assets/image (107).png>)

{% embed url="https://www.youtube.com/watch?v=-c7PXt7i37A" %}



### 表内外键

{% embed url="https://dev.mysql.com/doc/refman/8.0/en/create-table-foreign-keys.html" %}

{% embed url="https://pencilprogrammer.com/self-referencing-foreign-key-in-mysql/" %}

当表中自己和自己join时，需要在建表时就设置好外键

![](<../../.gitbook/assets/image (92).png>)

```sql
CREATE TABLE `employees` (
  `employee_id` int(11) NOT NULL,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) NOT NULL,
  `job_title` varchar(50) NOT NULL,
  `salary` int(11) NOT NULL,
  `reports_to` int(11) DEFAULT NULL,
  `office_id` int(11) NOT NULL,
  PRIMARY KEY (`employee_id`),
  KEY `fk_employees_offices_idx` (`office_id`),
  KEY `fk_employees_employees_idx` (`reports_to`),
  CONSTRAINT `fk_employees_managers` FOREIGN KEY (`reports_to`) REFERENCES `employees` (`employee_id`),
  CONSTRAINT `fk_employees_offices` FOREIGN KEY (`office_id`) REFERENCES `offices` (`office_id`) ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

### 插入Hierarchical Rows值

当两个表需要同时写入数据，而其中一张表又跟上一张表有FK约束关系，可以用`LAST_INSERT_ID`来获取前一张表中插入的ID，下图中，两个`LAST_INSERT_ID`的值都是一样的。

![](<../../.gitbook/assets/image (106).png>)

## Subquery

最简单的Subquery的例子就是只知道name而先要通过name去寻找对应的id，然后再通过这个id去另一个表中进行检索。具体执行的方法，可以从外向内写，如先把最终要的结果写出来，然后再去写WHERE后的subquery。也可以是从内向外写，就是先看看name对应的那个表能提供什么信息，然后再去写外包的query。

**Hint：**可以先单独执行subquery，确定返回的内容再说。

![Subquery返回的是单个值](<../../.gitbook/assets/image (110).png>)

![Subquery返回多个值](<../../.gitbook/assets/image (108).png>)

## 参考资料

{% embed url="https://www.youtube.com/watch?v=7S_tz1z_5bA" %}

