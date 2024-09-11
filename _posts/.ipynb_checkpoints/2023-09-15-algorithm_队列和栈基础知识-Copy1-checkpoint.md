---
layout: post
title: 队列和栈基础知识、225用队列实现栈、用栈实现队列
date: 2023-09-13 20:40:16
description: 代码随想录算法训练营第十天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---

>
>[232用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)
>
>[用栈实现队列代码随想录](https://programmercarl.com/0232.用栈实现队列.html#其他语言版本)
>
>[225用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/description/)
>
>[用队列实现栈代码随想录](https://programmercarl.com/0225.用队列实现栈.html#其他语言版本)
>

## 232.用栈实现队列

### 题目
请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：

实现 MyQueue 类：

`void push(int x)` 将元素 x 推到队列的末尾
`int pop()` 从队列的开头移除并返回元素
`int peek()` 返回队列开头的元素
`boolean empty()` 如果队列为空，返回 `true` ；否则，返回 `false`
说明：

你 只能 使用标准的栈操作 —— 也就是只有 `push to top`, `peek/pop from top`, `size`, 和 `is empty` 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 `list` 或者 `deque`（双端队列）来模拟一个栈，只要是标准的栈操作即可。


## 题解方法
- 采用两个队列模拟栈；
- 在需要pop时，将in栈中所有元素弹出至out栈中，则out栈；


# 题解代码
```python
class MyQueue:

    def __init__(self):
        self.stack_in = collections.deque()
        self.stack_out = collections.deque()

    def push(self, x: int) -> None:
        self.stack_in.append(x)

    def pop(self) -> int:
        if self.empty():
            return None

        if self.stack_out:
            return self.stack_out.pop()
        for i in range(len(self.stack_in)):
            node = self.stack_in.pop()
            self.stack_out.append(node)
        node_i = self.stack_out.pop()
        return node_i


    def peek(self) -> int:
        node_1 = self.pop()
        self.stack_out.append(node_1)
        return node_1

    def empty(self) -> bool:
        if len(self.stack_in)==0 and len(self.stack_out)==0:
            return True
        else:
            return False
```


## 225.用队列实现栈

## 题目
请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop` 和 `empty`）。

实现 `MyStack` 类：
- `void push(int x)` 将元素 `x` 压入栈顶。
- `int pop()` 移除并返回栈顶元素。
- `int top()` 返回栈顶元素。
- `boolean empty()` 如果栈是空的，返回 `true` ；否则，返回 `false` 。

## 题解
- 拿队列的实现栈 问题也在pop和top
- 每次pop时 将所有队列顶部数据重新弹出再放入一遍 保持队列顺序不变的情况下，重新来一遍；

## 题解代码
```python
from collections import deque
class MyStack:

    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)

    def pop(self) -> int:
        if self.empty():
            return None
        for i in range(len(self.queue)-1):
            node = self.queue.popleft()
            self.queue.append(node)
        return self.queue.popleft()

    def top(self) -> int:
        if self.empty():
            return None
        for i in range(len(self.queue)-1):
            node = self.queue.popleft()
            self.queue.append(node)
        node_i = self.queue.popleft()
        self.queue.append(node_i)
        return node_i

    def empty(self) -> bool:
        if not self.queue:
            return True
        else:
            return False

```

