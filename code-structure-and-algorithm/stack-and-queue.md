# Stack & Queue

## Stack \(LIFO, last in first out\)

A container to access, delete, insert data. Only has one top, which can **push** and **pop** data. O\(1\) for operations。可以理解为只能在一端进行插入或删除操作的python list列表

![](../.gitbook/assets/image%20%2821%29.png)

### 栈的python实现 <a id="&#x6808;&#x7684;python&#x5B9E;&#x73B0;"></a>

不需要自己定义，使用列表结构即可：

1. 进栈：append
2. 出栈：pop
3. 查看栈顶：li\[-1\] 直接取索引

### 栈的应用

#### 括号匹配问题：

给一个字符串，其中包含小括号、中括号、大括号，求该字符串中的括号是否匹配。比如：`()()[]{}`匹配，`([{()}])`匹配，`[](`不匹配，`[(])`不匹配：

```python
def check(exp):
    stack = [] # 创建栈
    for char in exp:
        if char in ['(', '[', '{']:
            stack.append(char)  # 压入栈
        elif char == ')':
            if stack and stack[-1] == '(':
                stack.pop()  # 弹出栈
            else:
                return False
        elif char == ']':
            if stack and stack[-1] == '[':
                stack.pop()
            else:
                return False
        elif char == '}':
            if stack and stack[-1] == '{':
                stack.pop()
            else:
                return False

    if not stack: #如果栈为空，说明括号全部匹配
        return True
    return False
```

## Queue \(FIFO, first in first out\)

Another container, has one enter and one end

![](../.gitbook/assets/image%20%2818%29.png)

