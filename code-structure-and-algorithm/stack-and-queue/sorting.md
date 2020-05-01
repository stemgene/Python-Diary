# Sorting

| Sorting | Best time complexity | Worst time complexity |
| :--- | :--- | :--- |
| Bubble Sort | O\(n\) | O\( $$n^2$$ \) |

## Bubble Sorting

* First iteration: horizontal i times, index \(0, n-1-j\)
* Second iteration: vertical j times, index \(0, n-1\)

![](../../.gitbook/assets/image%20%286%29.png)

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

if __name__ == "__main__":
  alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
  print(alist)
  bubble_sort(alist)
  print(alist)
```

## Selection Sorting

可以认为把一个序列分成两个，后面的是有序的，前面的是无序的，始终从前面无序的序列中找到最大值，放到后面有序的序列中。

![](../../.gitbook/assets/image%20%287%29.png)

