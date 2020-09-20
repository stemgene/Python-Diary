# Double Pointers

## Binary Search

### Example 1

**Algorithm:** 

1. Case 1: if nums\[mid\] == target → found! 
2. Case 2: if nums\[mid\] &lt; target→ if exists, the target should be in the right half of the array, left=mid+1 
3. Case 3: if nums\[mid\] &gt; target→ if exists, the target should be in the left half of the array, right=mid-1

**Principles:**

* Guarantee that the search space decreases after each iteration
* Guarantee that the target \(if exists\) is not ruled out when we change the value of L or R

```python
def binary_search(alist, target):
  # corner case
  if not alist:
    return None
  # left, right, mid are index
  left, right = 0, len(alist)-1
  while left <= right:
    mid = (left + right) // 2
    if alist[mid] == target:
      return mid
    elif alist[mid] > target:
      right = mid - 1
    else:
      left = mid + 1
  return None
```

有意思的一个情况是给出一个二维矩阵（排好序的），然后找出指定的target。解决办法是把二维矩阵拉伸为一维，然后执行binary search，再把找到的index还原为二维的表达方式。如给出一个\(4, 3\)的二维矩阵，n=4，m=3。

```python
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
[10, 11, 12]
```

假如9是target，并找到了index=8，怎么还原为二维表达方式\(2,2\)呢？公式就是`行=index//n`，`列=index%m`  

### Example 2: 找到最近似等于target的

How is it different from Q1?

1. You don’t know if mid is the answer or not
2. You need to include mid each time you get into halves

Algorithm:

1. Case 1: if nums\[mid\] == target → found!
2. Case 2: if nums\[mid\] &gt; target, if exists, the target should be in the left half, right=mid
3. Case 3: if nums\[mid \] &lt; target, if exists, the target should be in the right half, left=mid

```python
def find_closest(array, target):
   # corner case
    if not array:
        return None
    left, right = 0, len(array)-1
    while left < right-1:
        mid = (left+right)//2
        if array[mid] == target:
            return array[mid]
        elif array[mid] > target:
            # 因为是最近似，所以不是mid+1或mid-1，而是mid本身
            right = mid
        else:
            left = mid
    # 检验mid左右两边的差以确定哪个最近似        
    if abs(array[left]-target) > abs(array[right]-target):
        return array[right]
    else:
        return array[left]
    return None
 
find_closest([1,2,5,9],3)

```

