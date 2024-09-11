---
layout: post
title: 字符串：344反转字符串、541反转字符串2、替换数字、翻转字符串内单词、55右旋转字符串
date: 2023-09-12 20:40:16
description: 代码随想录算法训练营第八天
tags: Algorithm
giscus_comments: true
featured: false

toc:
    sidebar: left
---

>
>[反转字符串](https://leetcode.cn/problems/reverse-string/)
>
>[反转字符串代码随想录](https://programmercarl.com/0344.反转字符串.html#算法公开课)
>
>[替换数字](https://kamacoder.com/problempage.php?pid=1064)
>
>[替换数字代码随想录](https://programmercarl.com/kama54.替换数字.html#其他语言版本)
>
>[翻转单词](https://leetcode.cn/problems/reverse-words-in-a-string/description/)
>
>[右旋字符串](https://kamacoder.com/problempage.php?pid=1065)

# 344反转字符串

## 题目
编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

## 题解
- 现有方法：
    - 双指针：左右互换；
    - 遍历：循环前一半
    - 函数：reversed函数
    - 递推

# 题解代码
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l,r = 0,len(s)-1
        while l<r:
            s[l],s[r] = s[r],s[l]
            l+=1
            r-=1
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
