# Time & Space Complexity

![](<../.gitbook/assets/image (37).png>)

| Time       | Time Describe                                                                       | Space Describe  |
| ---------- | ----------------------------------------------------------------------------------- | --------------- |
| O(1)       | Constant, Fastest                                                                   | 不创建新的变量         |
| O(log n)   | <p>Goal for searching即不需要遍历所有structure；</p><p>while i &#x3C; n:</p><p>    i * 2</p> |                 |
| O(n)       | iterate所有item                                                                       | 创建一个新的size为n的数组 |
| O(n log n) | Goal for sorting                                                                    |                 |
| O(n^2)     | iterate 2次，应该优化                                                                     |                 |
| O(n!)      |                                                                                     |                 |

![](<../.gitbook/assets/image (38).png>)

## List time complexity

Python中的list存放的是变量内容的地址而不是变量内容的本身，如下图。所以对list取值要慢一些。insert和del的时间复杂度都是O(n)。另外Python中的list是栈stack的数据结构LIFO

![](<../.gitbook/assets/image (91).png>)

| **LIST**                |                         | **Big-O Efficiency** |
| ----------------------- | ----------------------- | -------------------- |
| **index\[]/assignment** | **`list[9]`**           | **O(1)**             |
| append                  | `list[9]=1`             | O(1)                 |
| **pop/pop(i)**          | ****                    | **O(1)/O(n)worst**   |
| insert                  | `insert(i,item)`        | O(n)                 |
| del                     |                         | O(n)                 |
| iteration               | `for i in list`         | O(n)                 |
| **contains**            | **`item in list`**      | **O(n)**             |
| get slice               | `list[x:y]`             | O(k), k=y-x+1        |
| del slice               | `del(list[x:y])`        | O(n)删后往前移            |
| set slice               | `list[0:3]=[1,2,3,4,5]` | O(n+k)先删n再补充k        |
| reverse                 |                         | O(n)                 |
| concatenate             | list(n)+list(k)         | O(k)                 |
| sort                    |                         | O(nlogn)             |
| multiply                | list(n) \* k            | O(nk)                |

## DICT time complexity

Python的dict是Hash table，they are not ordered and need resizing, which adds time complexity for more complicated functions. Use them for fast O(1) lookups, insertions, and deletions\


\


| **DICT Operation** |                  | **Big-O Efficiency** |
| ------------------ | ---------------- | -------------------- |
| copy               |                  | O(n)                 |
| get/set/del item   | `dict(key)`      | O(1)                 |
| contains           | `item in dict()` | O(1)                 |
| iteration          |                  | O(n)                 |
