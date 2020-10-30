# Time & Space Complexity

![](../.gitbook/assets/image%20%2837%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Time</th>
      <th style="text-align:left">Time Describe</th>
      <th style="text-align:left">Space Describe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">O(1)</td>
      <td style="text-align:left">Constant, Fastest</td>
      <td style="text-align:left">&#x4E0D;&#x521B;&#x5EFA;&#x65B0;&#x7684;&#x53D8;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">O(log n)</td>
      <td style="text-align:left">
        <p>Goal for searching&#x5373;&#x4E0D;&#x9700;&#x8981;&#x904D;&#x5386;&#x6240;&#x6709;structure&#xFF1B;</p>
        <p>while i &lt; n:</p>
        <p>i * 2</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">O(n)</td>
      <td style="text-align:left">iterate&#x6240;&#x6709;item</td>
      <td style="text-align:left">&#x521B;&#x5EFA;&#x4E00;&#x4E2A;&#x65B0;&#x7684;size&#x4E3A;n&#x7684;&#x6570;&#x7EC4;</td>
    </tr>
    <tr>
      <td style="text-align:left">O(n log n)</td>
      <td style="text-align:left">Goal for sorting</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">O(n^2)</td>
      <td style="text-align:left">iterate 2&#x6B21;&#xFF0C;&#x5E94;&#x8BE5;&#x4F18;&#x5316;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">O(n!)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

![](../.gitbook/assets/image%20%2838%29.png)

## List time complexity

Python中的list存放的是变量内容的地址而不是变量内容的本身，如下图。所以对list取值要慢一些。insert和del的时间复杂度都是O\(n\)。另外Python中的list是栈stack的数据结构LIFO

![](../.gitbook/assets/image%20%2891%29.png)

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

Python的dict是Hash table，they are not ordered and need resizing, which adds time complexity for more complicated functions. Use them for fast O\(1\) lookups, insertions, and deletions  


  


| **DICT Operation** |  | **Big-O Efficiency** |
| :--- | :--- | :--- |
| copy |  | O\(n\) |
| get/set/del item | `dict(key)` | O\(1\) |
| contains | `item in dict()` | O\(1\) |
| iteration |  | O\(n\) |

