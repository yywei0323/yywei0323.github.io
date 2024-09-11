---
layout: post
title: KMP算法-28字符串匹配+重复字符串
date: 2023-09-13 20:40:16
description: 代码随想录算法训练营第九天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---

>
>[28.strStr()](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
>
>[实现strStr()代码随想录](https://programmercarl.com/0028.实现strStr.html#思路)
>
>[459.重复字符串](https://leetcode.cn/problems/repeated-substring-pattern/submissions/538631105/)
>
>[重复字符串代码随想录](https://programmercarl.com/0459.重复的子字符串.html#其他语言版本)
>

## 28.字符串匹配

### 题目
给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串的第一个匹配项的下标（下标从 0 开始）。如果 needle 不是 haystack 的一部分，则返回 -1 。

## 题解方法——KMP
- next数组：最大相同前后缀数组 next\[i\]代表needle第i个字符的最大相同前后缀
- 获取next数组：
    - 判断当前字符串是否有重合
    - 如果没有回退到上一个字符的最大相同前后缀处

# 题解代码
```python
class Solution:
    def getnext(self,s):
        j = 0
        next_ = [0]*len(s)
        for i in range(1,len(s)):
            while j>0 and s[i]!=s[j]:##不一样 且不是初始值 则回退到上一个点
                j = next_[j-1]
            if s[i]==s[j]:
                j +=1
            next_[i] = j
        return next_

    def strStr(self, haystack: str, needle: str) -> int:
        if len(needle)==0:
            return 0
        next_ = self.getnext(needle)
        j = 0
        for i in range(len(haystack)):
            while j>0 and haystack[i]!=needle[j]:
                j = next_[j-1]
            if haystack[i]==needle[j]:
                j+=1
            if j==len(needle):
                return i-len(needle)+1
        return -1
```


## 459.重复字符串

## 题目
给定一个非空的字符串 s ，检查是否可以通过由它的一个子串重复多次构成

## 题解
- 方案1:移动匹配法：如果由重复字符串组成`s[1:]+s[-1]=s`成立；
- 方案2
    - 计算next_数组；如果最大相同前后缀 相差值 能%==0 说明刚好差一个原子值；

## 题解代码
```python
def main():
    data = list(input())
    for i in range(len(data)):
        if "a"<=data[i]<="z":
            continue
        else:
            data[i] = "number"
    print("".join(data))
    
if __name__ == '__main__':
    main()
```

