---
layout: post
title: 链表基础理论
date: 2023-09-8 20:40:16
description: 代码随想录算法训练营第三天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---


>[链表基础理论](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
>
>[203题目链接](https://leetcode.cn/problems/remove-linked-list-elements/)
>
>[203代码随想录](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
>
>[707题目链接](https://leetcode.cn/problems/design-linked-list/description/)
>
>[707代码随想录](https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)
>
>[206题目链接](https://leetcode.cn/problems/reverse-linked-list/submissions/535001438/)
>
>[206代码随想录](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)


## 链表基础知识笔记

**链表示意图**
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-08/1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### 单链表（如上图）
```python
class linknode:
    def __init__(self,val,next = None):
        self.val = val
        self.next = next
```

### 双链表
```python
class blinknode:
    def __init__(self,val,next = None,front = None):
        self.val = val
        self.next = next
        self.front = front
```

### 链表操作

#### 删除节点
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-08/2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### 加入节点

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-08/3.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


## 203.移除链表元素

## 题目
**给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。**

### 重点内容
- 设置虚拟头节点，在删除头节点时会更便利；
- 考虑链表遍历的条件和范围


```python
def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
    node_1 = ListNode()
    node_1.next = head
    curr = node_1
    while curr.next:
        if curr.next:
            if curr.next.val == val:
                curr.next = curr.next.next
                continue
        curr = curr.next
    return node_1.next
```

## 707 设计链表

### 题目
**你可以选择使用单链表或者双链表，设计并实现自己的链表。
单链表中的节点应该具备两个属性：val 和 next 。val 是当前节点的值，next 是指向下一个节点的指针/引用。
如果是双向链表，则还需要属性 prev 以指示链表中的上一个节点。假设链表中的所有节点下标从 0 开始。**

**实现 MyLinkedList 类：**
- MyLinkedList() 初始化 MyLinkedList 对象。
- int get(int index) 获取链表中下标为 index 的节点的值。如果下标无效，则返回 -1 。
- void addAtHead(int val) 将一个值为 val 的节点插入到链表中第一个元素之前。在插入完成后，新节点会成为链表的第一个节点。
- void addAtTail(int val) 将一个值为 val 的节点追加到链表中作为链表的最后一个元素。
- void addAtIndex(int index, int val) 将一个值为 val 的节点插入到链表中下标为 index 的节点之前。如果 index 等于链表的长度，那么该节点会被追加到链表的末尾。如果 index 比长度更大，该节点将 不会插入 到链表中。
- void deleteAtIndex(int index) 如果下标有效，则删除链表中下标为 index 的节点。

### 重点内容：
- 基本可以自己复现
- 问题1：可以设置self.size 遍历循环
- 遍历到index前一个和index当前那一个的公式不同
- get 和 delete的范围\[0,size\) add\_index范围是\[0,index\]

```python
curr = self.dummy_node
for i in range(curr):
    curr = curr.next
### 结束时 curr为index的前一个
```

### 最终解答：
```python
class Node:
    def __init__(self,val=0 ,next = None):
        self.val = val
        self.next = next

class MyLinkedList:
    def __init__(self):
        self.headnode = Node()
        self.size = 0

    def get(self, index: int) -> int:
        if index<0 or index>=self.size:
            return -1
        curr = self.headnode.next
        for i in range(index):
            curr = curr.next
        return curr.val

    def addAtHead(self, val: int) -> None:
        node_1 = Node(val)
        node_1.next = self.headnode.next
        self.headnode.next = node_1
        self.size = self.size+1

    def addAtTail(self, val: int) -> None:
        node_1 = Node(val)
        curr = self.headnode
        while curr.next:
            curr = curr.next
        curr.next = node_1
        self.size = self.size+1

    def addAtIndex(self, index: int, val: int) -> None:
        if index<0 or index>self.size:
            return 
        node_1 = Node(val)
        curr = self.headnode
        for i in range(index):
            curr = curr.next
        node_1.next = curr.next
        curr.next = node_1
        self.size =self.size+1


    def deleteAtIndex(self, index: int) -> None:
        if index>=0 and index<self.size:
            curr = self.headnode
            for i in range(index):
                curr = curr.next
            curr.next = curr.next.next
            self.size = self.size-1
        else:
            return
```

## 206反转链表

### 题目
**给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。**

### 重点：
- 第一遍没做出来，但其实只要想起来**双指针**就会了;
- python的迭代和递归区别不太大

### 最终解答：
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        curr = head
        pre = None
        while curr:
            tmp = curr.next
            curr.next = pre
            pre = curr
            curr = tmp
        return pre
```