# String & Regexp

<table><thead><tr><th width="169.00000000000003">Useful Functions</th><th width="304.91739894551847">SQL</th><th>Result</th></tr></thead><tbody><tr><td>LENGTH</td><td><code>SELECT LENGTH('LearnSQL.com');</code></td><td>12</td></tr><tr><td>LOWER</td><td><code>SELECT LOWER('LEARNSQL.com');</code></td><td>learnsql.com</td></tr><tr><td>UPPER</td><td><code>SELECT UPPER('LearnSQL.com');</code></td><td>LEARNSQL.COM</td></tr><tr><td>SUBSTRING</td><td><code>SELECT SUBSTRING('LearnSQL.com', 9);</code><br><code>SELECT SUBSTRING('LearnSQL.com', 0,6);</code></td><td>.com<br><br><br>Learn 第一个数字是开始位置，第二个数字是长度</td></tr><tr><td>LEFT从左侧截取字符</td><td><code>SELECT LEFT(name, 1)</code></td><td>D</td></tr><tr><td>RIGHT从右侧截取字符</td><td>SELECT RIGHT(name, length(name) - 1)</td><td>avid</td></tr><tr><td>REPLACE</td><td><code>SELECT REPLACE('LearnSQL.com', 'SQL', 'Python');</code></td><td>LearnPython.com</td></tr><tr><td>CONCAT</td><td><code>CONCAT(str1, str2)</code></td><td>str1str2</td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

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
