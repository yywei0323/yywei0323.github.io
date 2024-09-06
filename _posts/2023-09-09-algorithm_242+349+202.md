---
layout: post
title: 哈希表基础;242有效字母异位;349两个数组交集;202快乐数
date: 2023-09-10 20:40:16
description: 代码随想录算法训练营第六天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---


>[哈希表基础理论](https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E5%93%88%E5%B8%8C%E8%A1%A8)
>[242有效字母异位词题](https://leetcode.cn/problems/valid-anagram/description/)
>
>[242代码随想录解析](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
>
>[349两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)
>
>[349代码随想录解析]
(https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
>
>[202快乐数](https://leetcode.cn/problems/happy-number/)
>
>[202代码随想录解析](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)



# 哈希表基础理论
***当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法***

python中重要和字典相关的语句
```python
num = res.get(num,0)+1
##res.get(num,0) 如果存在num，则获取该数值，如果不存在该key，则赋值为0
```

# 242有效字母异位词
## 题目

**给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。
注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。**

## 题解

**对于Python来说 有两种解决方案**
1. 直接采用python的collections.counter
2. 采用哈希表 统计26字母的频次

## 解法代码
```python
###解法一：counter
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        s_dict = dict(collections.Counter(s))
        t_dict = dict(collections.Counter(t))
        if s_dict==t_dict:
            return True
        else:
            return False
```

```python
##解法二
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0]*26 ##哈希表
        for i in s:
            record[ord(i)-ord("a")]+=1
        for i in t:
            record[ord(i)-ord("a")]-=1
        for i in record:
            if i!=0:
                return False
        return True
```


# 349两个数组的交集
## 题目
**给定两个数组 nums1 和 nums2 ，返回 它们的 交集。
输出结果中的每个元素一定是 唯一 的。我们可以 不考虑输出结果的顺序 。**

## 题解：
1. 采用字典和集合统计
2. 直接使用集合

```python
##用集合方法
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```

## 202快乐数
### 题目
**编写一个算法来判断一个数 n 是不是快乐数。
「快乐数」 定义为：
    - 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
    - 然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
    - 如果这个过程 结果为 1，那么这个数就是快乐数。
    - 如果 n 是 快乐数 就返回 true ；不是，则返回 false。
**

## 题解
要点在**如果不是快乐数，可能无限循环始终变不到1**
因此，只需要判断结果是否有重复出现即可

## 解题代码
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        curr = n
        res = {}
        while curr!=1 and res.get(curr,0)<2:
            num = 0
            for i in str(curr):
                num = num + int(i)**2
            curr = num
            res[num] = res.get(num,0)+1
        if curr==1:
            return True
        else:
            return False
```