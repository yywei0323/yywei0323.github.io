---
layout: post
title: 28字符串匹配；重复字符串；
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
    - 判断当前字符串是否

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
# 替换数字

## 题目
给定一个字符串 s，它包含小写字母和数字字符，请编写一个函数，将字符串中的字母字符保持不变，而将每个数字字符替换为number。 例如，对于输入字符串 "a1b2c3"，函数应该将其转换为 "anumberbnumbercnumber"。

## 题解
- 字符串不能直接在原位修改转为列表
- 字符串本身可以比大小

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

# 55.右旋转字符串
## 题目
字符串的右旋转操作是把字符串尾部的若干个字符转移到字符串的前面。给定一个字符串 s 和一个正整数 k，请编写一个函数，将字符串中的后面 k 个字符移到字符串的前面，实现字符串的右旋转操作。

例如，对于输入字符串 "abcdefg" 和整数 2，函数应该将其转换为 "fgabcde"。


## 题解：
- 思路1：直接重新拼接字符串 从`k%len`划分开拼接；
- 思路2：反转两次=没有反转-> 整体反向+前后分别反向


## 题解代码
```python
num = input()
str_ = input()
num = int(num)

def righerreverse(num,str_):
    str_ = str_[::-1]
    res_str = str_[0:num][::-1]+str_[num:][::-1]
    return res_str

res_str = righerreverse(num,str_)
print(res_str)
```
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
