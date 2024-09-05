---
layout: post
title: 977.有序数组的平方；209.长度最小的子序列
date: 2023-09-7 20:40:16
description: 代码随想录算法训练营第二天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---


>[977题链接](https://leetcode.cn/problems/squares-of-a-sorted-array/)
>
>[代码随想录链接](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html#%E6%80%9D%E8%B7%AF)
>
>[209题链接](https://leetcode.cn/problems/minimum-size-subarray-sum/submissions/534560400/)
>
>[代码随想解答](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)

## 今日任务
1. 八股背诵：HTTP部分：HTTPS和HTTP区别、UDP和TCP（拥塞控制、滑动窗口）、
2. 代码随想录补打卡day1、day2；
3. 毕设实验；

## 第一遍解题难点：
- 整理出来了实际是比较绝对值大小；
- 没有考虑到**两边大中间小**的特征，惯性思维想遍历，没想到可以从**两端**使用指针；
- 在思考如何赋值的时候忘记了**python复制语句**；

## 最终解答：
```python
def sortedSquares(self, nums: List[int]) -> List[int]:
    res = ['inf']*len(nums) ##先创建相应的空间
    l,r,i = 0,len(nums)-1,len(nums)-1 ##l,r分别为两端指针；i是赋值指针
    while l<=r:
        if abs(nums[l])>=abs(nums[r]):
            res[i] = nums[l]*nums[l]
            l = l+1
        else:
            res[i] = nums[r]*nums[r]
            r = r-1
            i = i-1
            return res
```

## 209

### 第一遍解题难点：
- 理解错了题意：是大于等于的连续子数组，不是等于的连续子数组；
- 双指针的滑动窗口：只动了一边，效率低；

### 最终解答

```python
def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        right = 0
        min_len = float('inf')
        sum_ = 0
        while right<len(nums):
            sum_=sum_+nums[right]

            while sum_>=target:
                min_len = min(min_len,right-left+1)
                sum_ = sum_-nums[left]
                left = left+1
            right = right+1

        if min_len==float('inf'):
            return 0
        else:
            return min_len
```
