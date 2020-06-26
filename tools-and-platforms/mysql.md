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

**\`\`**



