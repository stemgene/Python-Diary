# Time Complexity

![](../.gitbook/assets/image%20%2810%29.png)

![](../.gitbook/assets/image%20%2811%29.png)

## List time complexity

| **LIST** |  | **Big-O Efficiency** |
| :--- | :--- | :--- |
| **index\[\]/assignment** | **`list[9]`** | **O\(1\)** |
| append | `list[9]=1` | O\(1\) |
| **pop/pop\(i\)** | \*\*\*\* | **O\(1\)/O\(n\)worst** |
| insert | `insert(i,item)` | O\(n\) |
| del |  | O\(n\) |
| iteration | `for i in list` | O\(n\) |
| **contains** | **`item in list`** | **O\(n\)** |
| get slice | `list[x:y]` | O\(k\), k=y-x+1 |
| del slice | `del(list[x:y])` | O\(n\)删后往前移 |
| set slice | `list[0:3]=[1,2,3,4,5]` | O\(n+k\)先删n再补充k |
| reverse |  | O\(n\) |
| concatenate | list\(n\)+list\(k\) | O\(k\) |
| sort |  | O\(nlogn\) |
| multiply | list\(n\) \* k | O\(nk\) |

## DICT time complexity

| **DICT Operation** |  | **Big-O Efficiency** |
| :--- | :--- | :--- |
| copy |  | O\(n\) |
| get/set/del item | `dict(key)` | O\(1\) |
| contains | `item in dict()` | O\(1\) |
| iteration |  | O\(n\) |

