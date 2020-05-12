# Sorting

| Sorting | Best time complexity | Worst time complexity |
| :--- | :--- | :--- |
| Bubble Sort | O\(n\) | O\( $$n^2$$ \) |
| Selection Sort | O\( $$n^2$$ \) | O\( $$n^2$$ \) |
| Insertion Sort | O\(n\) | O\( $$n^2$$ \) |
| Shell Sort | O\( $$n^{1.3}$$ \) | O\( $$n^2$$ \) |
| **Quick Sort** | **O\(nlogn\)** | **O\(** $$n^2$$ **\)** |
| Merge Sort | O\(nlogn\) | O\(nlogn\) |
| Binary Search | O\(1\) | O\(nlogn\) |

## Bubble Sorting

* First iteration: horizontal i times, index \(0, n-1-j\)
* Second iteration: vertical j times, index \(0, n-1\)

![](../.gitbook/assets/image%20%2820%29.png)

```python
#先写内层循环i（横向），再写纵向的外层循环j
def bubble_sort(alist):
  n = len(alist)
  for j in range(n-1):
    for i in range(0, n-1-j): #start from 0, the last digit is n-1
      if alist[i] > alist[i+1]:
        alist[i], alist[i+1] = alist[i+1], alist[i]

if __name__ == "__main__":
  alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
  print(alist)
  bubble_sort(alist)
  print(alist)
  
>>>[54, 26, 93, 17, 77, 31, 44, 55, 20]
>>>[17, 20, 26, 31, 44, 54, 55, 77, 93]
```

### Optimized bubble sort--for already sorted at the end of sequence

```python
#先写内层循环i（横向），再写纵向的外层循环j
def bubble_sort(alist):
  n = len(alist)
  for j in range(n-1):
    count = 0
    for i in range(0, n-1-j): #start from 0, the last digit is n-1
      if alist[i] > alist[i+1]:
        alist[i], alist[i+1] = alist[i+1], alist[i]
        count += 1
    if count == 0: #代表后面的已经排好序了
      return
```

## Selection Sorting

可以认为把一个序列分成两个，后面的是有序的，前面的是无序的，始终从前面无序的序列中找到最大值，放到后面有序的序列中。

每一个数字对应着index，每一轮检索时寻找最大值，标记出最大值的index，然后和最后的index互换

* 第1趟比较：拿第1个元素依次和它后面的每个元素进行比较，如果第1个元素大于后面某个元素，交换它们，经过第1趟比较，数组中最小的元素被选出，它被排在第一位。
* 第2趟比较：拿第2个元素依次和它后面的每个元素进行比较，如果第2个元素大于后面某个元素，交换它们，经过第2趟比较，数组中第2小的元素被选出，它被排在第二位。
* ......
* 第n-1趟比较：第n-1个元素和第n个元素作比较，如果第n-1个元素大于第n个元素，交换它们。

![](../.gitbook/assets/image%20%2817%29.png)

![](../.gitbook/assets/image%20%2814%29.png)

```python
def selection_sort(alist):
  n = len(alist)
  for j in range(0, n-1): # j: 0~n-2
    min_index = j
    for i in range(j+1,n):
      if alist[min_index] > alist[i]:
        min_index = i
    alist[j], alist[min_index] = alist[min_index], alist[j]

if __name__ == "__main__":
  alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
  print(alist)
  selection_sort(alist)
  print(alist)
  
>>>[54, 26, 93, 17, 77, 31, 44, 55, 20]
>>>[17, 20, 26, 31, 44, 54, 55, 77, 93]
```

## Insertion Sorting

把一个数列分为前后两个，前面的是有序的，后面的是原有的无序的。每一轮遍历都将新的数字和前面的有序序列的每一个元素比较，直到找到正确的位置插入。Selection Sorting操作的是无序序列（每一轮找到无序序列的极值），而Insertion Sorting操作的是有序序列的一侧。

![](../.gitbook/assets/image%20%2810%29.png)

```python
def insertion_sort(alist):
  n = len(alist)
  # 从右边的无序序列中取出多少个元素执行
  for j in range(1, n):
    # j = [1, 2, 3, ..., n-1]
    # i 代表内层循环起始值
    i = j
    # 执行从右边的无序序列中取出第一个元素，即i位置的元素，然后将其插入到前面的正确位置中
    while i > 0:
      if alist[i] < alist[i-1]:
        alist[i], alist[i-1] = alist[i-1], alist[i]
        i -= 1
      else:
        break
```

```python
def sortArray(alist): 
    n = len(alist) 
    for j in range(1, n): 
        for i in range(j, 0, -1): 
            if alist[i] < alist[i - 1]: 
                alist[i-1], alist[i] = alist[i], alist[i-1] 
    return alist
```

This spacing is termed as **interval**. First round take the interval = 4

![](../.gitbook/assets/image%20%2823%29.png)

![](../.gitbook/assets/image%20%2821%29.png)

Then take interval = 2

![](../.gitbook/assets/image%20%2830%29.png)

![](../.gitbook/assets/image%20%289%29.png)

Finally, take interval = 1, just like Insertion Sorting

![](../.gitbook/assets/image%20%284%29.png)

```python
def shell_sort(alist):
  n = len(alist)
  gap = n // 2

  # gap变化到0之前，插入算法执行的次数
  while gap > 0:
    #插入算法，与普通的插入算法的区别就是gap步长
    for j in range(gap, n):
      # j = [gap, gap+1, gap+2,...,n-1]
      i = j
      while i > 0:
        if alist[i] < alist[i-gap]:
          alist[i], alist[i-gap] = alist[i-gap], alist[i]
          i -= gap
        else:
          break
    # 缩短gap步长
    gap //= 2
```

## Quicksort

[视频讲解](https://www.youtube.com/watch?v=Vs4SYLLEeI0&list=PLC664nq_h8b_q8Hjq_q8fbst1TO1AKKz-&index=39)

1. 从第一个数开始，将之暂存至`mid_value`的临时变量中，设置`low_index`和`high_index`分别指向左右两端。
2. 从右侧开始比较，如果`high>mid`, `high_index`向左移一步，否则high移到`low_index`上。
   * 在移动过程中的原则：因为起初把第一个值寄存到`mid_value`中，所以`low_index`就空了，然后low和high移来移去始终空着一个位置。对于已经空了的位置，该位置对应的index是不动的，直到有数值移过来为止。
   * 如果遇到相等的情况，所有值放到`mid_valude`的同一边，要么大要么小。 
3. `low_index`向右，`high_index`向左，重复上述过程，直到`low_index==high_index`，然后把`mid_value`赋给这个位置。
4. 分别重复做mid\_value左右两边的序列。

![](../.gitbook/assets/image%20%2818%29.png)

```python
def quick_sort(alist, first, last):
  if first == last:
    return
    
  mid_value = alist[first]
  n = len(alist)
  low = first
  high = last
  
  while low < high:
    # high 左移
    while low < high and alist[high] >= mid_value:
      high -= 1
    alist[low] = alist[high]
#    low += 1

    # low 右移
    while low < high and alist[low] < mid_value:
      low += 1
    alist[high] = alist[low]
    #high -= 1
    # 从循环推出时，low==high
    alist[low] = mid_value

    # 对low左边的列表执行快速排序
    quick_sort(alist, first, low-1)
    # 对low右边的列表执行快速排序
    quick_sort(alist, low+1, last)

if __name__ == "__main__":
  alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
  print(alist)
  quick_sort(alist, 0, len(alist)-1)
  print(alist)
```

## Merge Sorting

[视频讲解](https://www.youtube.com/watch?v=ti5UyToBOeE&list=PLC664nq_h8b_q8Hjq_q8fbst1TO1AKKz-&index=43)

1. 先分割，再合并。
2. 合并时需要引入left和right的index，这两个index分别在两组排好序列的最左端，然后比较left和right的大小，移走的index向右走一步。

![](../.gitbook/assets/image%20%286%29.png)

```python
def merge_sort(alist):
  n = len(alist)
  if n <= 1:
    return alist
  # 拆分过程
  mid = n // 2
  # left， right采用归并排序后形成的有序的新的列表
  left_li = merge_sort(alist[:mid]) # 生成新的list, 回头left
  right_li = merge_sort(alist[mid:])

  # 合并过程
  # 将两个有序的子序列合并成一个整体
  # merge(left, right)
  left_pointer, right_pointer = 0, 0
  result = []
  
  while (left_pointer < len(left_li)) and (right_pointer < len(right_li)):
    if left_li[left_pointer] < right_li[right_pointer]:
      result.append(left_li[left_pointer])
      left_pointer += 1
    else:
      result.append(right_li[right_pointer])
      right_pointer += 1
  result += left_li[left_pointer:]
  result += right_li[right_pointer:]
  return result

if __name__ == "__main__":
  alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
  print(alist)
  sorted_li = merge_sort(alist)
  print(sorted_li)
```

## 

