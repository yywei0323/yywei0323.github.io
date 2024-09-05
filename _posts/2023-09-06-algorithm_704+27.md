---
layout: post
title: 704.二分查找(红蓝模板法); 27. 移除元素(双指针法)
date: 2023-09-6 20:40:16
description: 代码随想录算法训练营第一天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---

>[704题链接](https://leetcode.cn/problems/binary-search/description/)
>[二分查找](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)
>
>二分查找红蓝法笔记：
 [二分查找为什么总是写错？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1d54y1q7k7/?spm_id_from=333.999.0.0&vd_source=15bd621bc528dc5761beb2a6637d341c)
>
>[34. 在排序数组中查找元素的第一个和最后一个位置 - 力扣（LeetCode）](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/solutions/967331/lan-hong-hua-fen-fa-dan-mo-ban-miao-sha-e7r40/)
>
>[27题链接](https://leetcode.cn/problems/remove-element/submissions/534439498/)
>
>[移除元素](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)

## 74题：二分查找红蓝法步骤：

1. 建模
2. 套入算法
3. 增加判断标准

## 建模示例：

1. 起始状态

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-01/1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


2. 终止状态
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-01/2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2023-09-01/2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

```python
##查找的范围为[0,N)
l,r = -1,N
while (l+1)!=r: ##循环终止的条件：红蓝边界重合；左右指针相邻
	mid = (l+r)//2 ##mid是左右指针的靠前的中间值
	if fuhe蓝色条件A:
		l = mid
	else:
		r = mid
##最终返回什么值由模型决定
```

## 注意事项：

1. 循环停止的判断条件：统一写成 l+1<r。 如果跨数组，或者跨区域，则必须选择l+1<r （例题：[1855. 下标对中的最大距离](https://leetcode.cn/problems/maximum-distance-between-a-pair-of-values/)）
2. 搜索完毕的特殊状态：l=首元素下标-1；全部为红色

## 技巧：

1. **排序**（对数组首先进行排序 排序完成后再进行查找 可以根据条件决定排序的方向）
    1. 例题：[1608. 特殊数组的特征值](https://leetcode.cn/problems/special-array-with-x-elements-greater-than-or-equal-x/)
2. **构造二分查找区间：**target和整数直接的必要条件关系，利用关系进行夹逼
    1. 例题：[69. x 的平方根](https://leetcode.cn/problems/sqrtx/)
3. 区间边界设定和边界值颜色是否确定有关；不确定就移动一格
4. **逐步缩小二分查找区间**
    1. 例题：[1855. 下标对中的最大距离](https://leetcode.cn/problems/maximum-distance-between-a-pair-of-values/)、[1300. 转变数组后最接近目标值的数组和](https://leetcode.cn/problems/sum-of-mutated-array-closest-to-target/)
5. **多维度向量二分查找：一个向量为主键进行排序**
    1. 主维度从小到大排序，从属维度从大到小排序 例如：[354. 俄罗斯套娃信封问题](https://leetcode.cn/problems/russian-doll-envelopes/)
    2. 主维度从小到大排序，从属维度动态插入排序 例如：[1847. 最近的房间](https://leetcode.cn/problems/closest-room/)


## 27题：双指针法
### 快慢指针 模板 忘了 所以第一遍写的很困难

```python
fast = 0 ##快指针 用于遍历
slow = 0 ##慢指针 用于筛选条件（一般为符合条件的）
while fast<len(nums):
    if nums[fast]!=val: ##满足条件
        nums[slow] = nums[fast]
        slow = slow+1 ##slow慢就是因为要符合条件才移动
    fast = fast+1 ##fast快是因为任何时间都会移动
```

