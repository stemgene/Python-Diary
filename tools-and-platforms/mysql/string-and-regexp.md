# String & Regexp

| Useful Functions | SQL                                                                                                             | Result                                           |
| ---------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| LENGTH           | `SELECT LENGTH('LearnSQL.com');`                                                                                | 12                                               |
| LOWER            | `SELECT LOWER('LEARNSQL.com');`                                                                                 | learnsql.com                                     |
| UPPER            | `SELECT UPPER('LearnSQL.com');`                                                                                 | LEARNSQL.COM                                     |
| SUBSTRING        | <p><code>SELECT SUBSTRING('LearnSQL.com', 9);</code><br><code>SELECT SUBSTRING('LearnSQL.com', 0,6);</code></p> | <p>.com<br><br><br>Learn 第一个数字是开始位置，第二个数字是长度</p> |
| LEFT从左侧截取字符      | `SELECT LEFT(name, 1)`                                                                                          | D                                                |
| RIGHT从右侧截取字符     | SELECT RIGHT(name, length(name) - 1)                                                                            | avid                                             |
| REPLACE          | `SELECT REPLACE('LearnSQL.com', 'SQL', 'Python');`                                                              | LearnPython.com                                  |
| CONCAT           | `CONCAT(str1, str2)`                                                                                            | str1str2                                         |
|                  |                                                                                                                 |                                                  |

## LIKE Operator - Pattern matching

* \_ : replace any single character.
* % : replace any number of characters (including 0 characters)

```sql
// Fetch all names that start with any letter followed by 'atherine'
SELECT name FROM names WHERE name LIKE '_atherine';

// Fetch all names that end with 'a';
SELECT name FROm names WHERE name LIKE '%a';

like ‘%or%’     //含有or的元素
like ‘_r%’        //第二位是r，_表示单个字符
like ‘a%o’       //以a开头o结尾的
```
