---
layout: post
title: 24题目链接;19题链接;面试题02.07链表相交;环形链表题目链接
date: 2023-09-10 20:40:16
description: 代码随想录算法训练营第四天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---


>[24题目链接](https://leetcode.cn/problems/swap-nodes-in-pairs/description/)
>
>[24题代码随想录讲解](https://programmercarl.com/0024.两两交换链表中的节点.html#思路)
>
>[19题链接](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)
>
>[19题代码随想录](https://programmercarl.com/0019.删除链表的倒数第N个节点.html)
>
>[面试题02.07链表相交]
(https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/description/)
>
>[面试0207代码随想录链接](https://programmercarl.com/面试题02.07.链表相交.html#其他语言版本)
>
>[环形链表题目链接](https://leetcode.cn/problems/linked-list-cycle-ii/)
>
>[环形链表代码随想录链接](https://programmercarl.com/0142.环形链表II.html#思路)



# # 24题题解
## 题目
给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

## 解题思路
- 确定使用虚拟头结点，防止头节点在循环中丢失；
- 递归版本：永远只交换前两个节点 头节点循环；
- 步骤清晰：确认curr是前一个节点还是后一个节点；


## 解决代码
```python
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_node = ListNode(next = head)
        pre = dummy_node
        curr = head

         if not curr or not curr.next:
            return head
        ###如果有少于2个节点 则不用循环

        while curr and curr.next:
            tmp = curr.next.next
            ###固定下一个循环的起始

            pre.next = curr.next
            curr.next.next = curr
            curr.next = tmp
            ###交换节点

            pre = curr
            curr = tmp
            ##循环推进
        return dummy_node.next
```

##


# 19题题解

## 题目
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

## 题解
- 双指针同时追逐
- 保证慢指针少走一步：我选择的是让fast走head-none;slow走dummy_node->最后一个node

## 题解代码
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_node = ListNode(next = head)
        slow = dummy_node
        fast = head
        for i in range(n):
            fast = fast.next
        while fast:
            fast = fast.next
            slow = slow.next

        if slow.next:
            tmp = slow.next
            slow.next = slow.next.next
            tmp.next = None
            ##删除节点

        return dummy_node.next
```


# 面试0207
## 题目
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-09/1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
图示两个链表在节点 c1 开始相交：
题目数据 保证 整个链式结构中不存在环。
注意，函数返回结果后，链表必须 保持其原始结构 。

## 题解
- 思路一：最简单的思路是：通过遍历获取两条链表的长度；从共同长度倒着找相交节点如图
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-09/2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
- 思路二：但更简便的方法是：轮流遍历两条链表 如果相遇，一定是节点，如果无法相遇，会在a+b时，返回None,则证明没中间节点

## 思路二代码
```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        A = headA
        B = headB
        while A!=B:
            A = A.next if A else headB
            B = B.next if B else headA
        return A
```

# 环形链表判断
## 题目：
给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

不允许修改 链表。

## 题解：
- 重点1：**快慢指针速度相差1倍，一定能相遇。**只要能相遇，则说明必定有环；
- 重点2：**快慢指针相遇后，从起点开始速度相同，相遇点即为起始点；**
- 重点3：**快慢指针相遇一定慢指针只差一环** x=(n-1)(y+z)+z

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-09/3.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## 题解代码：
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_node = ListNode(next = head)
        slow = head
        fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if slow == fast:##相遇有环
                fast = head
                while fast!=slow:
                    fast = fast.next
                    slow = slow.next
                return slow
        return None ##不相遇无环
```
