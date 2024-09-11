---
layout: post
title: 逆波兰表达式、滑动窗口最大值、前 K 个高频元素 
date: 2023-09-15 20:40:16
description: 代码随想录算法训练营第十一天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---

>
>[逆波兰表达式题目](https://leetcode.cn/problems/evaluate-reverse-polish-notation/description/)
>
>[逆波兰表达式代码随想录](https://programmercarl.com/0150.逆波兰表达式求值.html#其他语言版本)
>
>[滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)
>
>[滑动窗口最大值代码随想录](https://programmercarl.com/0239.滑动窗口最大值.html)
>
>[前K个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/description/)
>
>[前K个高频元素代码随想录](https://programmercarl.com/0347.前K个高频元素.html)
>

## 150.逆波兰表达式求值

### 题目
给你一个字符串数组 tokens ，表示一个根据 逆波兰表示法 表示的算术表达式。
请你计算该表达式。返回一个表示表达式值的整数。
注意：
有效的算符为 '+'、'-'、'*' 和 '/' 。
- 每个操作数（运算对象）都可以是一个整数或者另一个表达式。
- 两个整数之间的除法总是 向零截断 。
- 表达式中不含除零运算。
- 输入是一个根据逆波兰表示法表示的算术表达式。
- 答案及所有中间计算结果可以用 32 位 整数表示。


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

