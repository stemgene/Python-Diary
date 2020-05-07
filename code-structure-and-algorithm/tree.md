# Tree

## Binary Search

![](../.gitbook/assets/image%20%2811%29.png)

```python
# 递归版本
def binary_search(alist, item):
  n = len(alist)
  if n > 0:
    mid = n//2
    if alist[mid] == item:
      return True
    elif item < alist[mid]:
      return binary_search(alist[:mid], item)
    else:
      return binary_search(alist[mid+1:], item)
  return False

if __name__ == "__main__":
  alist = [17, 20, 26, 31, 44, 54, 55, 77, 93]
  print(binary_search(alist, 55))
  print(binary_search(alist, 100))
  
>>> True
>>> False
```

```python
# 非递归版本
def binary_search(alist, item):
  n = len(alist)
  first = 0
  last = n-1
  while first <= last:
    mid = (first + last) // 2
    if alist[mid] == item:
      return True
    elif item < alist[mid]:
      last = mid - 1
    else:
      first = mid + 1
  return False

if __name__ == "__main__":
  alist = [17, 20, 26, 31, 44, 54, 55, 77, 93]
  print(binary_search(alist, 55))
  print(binary_search(alist, 100))
```

## Tree

* 每个节点都有零个或多个子节点
* 没有父节点的节点成为跟节点
* 每一个非根节点有且只有一个父节点
* 除了根节点外，每个子节点可以分为多个不相交的子树

### Binary Tree

![](../.gitbook/assets/image%20%2828%29.png)

* 每个节点最多有两个子树，被称为left subtree和right subtree
* 在二叉树的第i层上至多有 $$2^{i-1}$$ 个节点（横向的最多节点数）
* 深度为k的二叉树至多有 $$2^k-1$$ 个节点
* 对于任意一棵二叉树，如果其叶节点数为 $$N_0$$（最底层的叶子数，即图中的8,9,10,11,12,7,共6个） ，而度数为2的节点总数为$$N_2$$（即图中的1, 2, 3, 4, 5, 个数为5），则 $$N_0=N_2+1$$ 
* 具有N个节点的完全二叉树的深度必为 $$log_2(n+1)$$ 
* 对于完全二叉树，若从上至下，从左至右编号，则编号为i的节点，其左子树编号必为2i，右子树编号必为2i+1，父树的编号为i/2（i=1时为根，除外）

