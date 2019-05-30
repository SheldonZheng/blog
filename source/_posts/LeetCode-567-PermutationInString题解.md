---
title: LeetCode.567.PermutationInString题解
date: 2019-05-30 17:13:35
categories:
- LeetCode题解
tags: 
- LeetCode
- String
---

## LeetCode 567 Permutation in String 题解



[题目地址](https://leetcode.com/problems/permutation-in-string/)

### Description:

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

 

**Example 1:**

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

 

**Note:**

1. The input strings only contain lower case letters.
2. The length of both given strings is in range [1, 10,000].



### 解:

由于要求是s1的任意排列都可以，所以简单地扫描是不行的，如果计算出s1的所有排列挨个扫描，那太慢了

其实就是比较在相同长度的两个字符串里字符出现的频率，所以定义两个数组一个存s1里所有字符出现的频率，另外一个滑动扫描s2，每前进一步判断一次是否满足条件，前进一步把开头的字符删掉





### Code:

```java
public boolean checkInclusion(String s1, String s2) {
        if (s1 == null || s2 == null)
            return false;
        if (s1.length() == 0) {
            return true;
        }
        if (s1.length() > s2.length()) {
            return false;
        }
        int[] ba = new int[26];
        int[] slideArray = new int[26];

        int slideWidth = s1.length();

        int slideS = 0;
        int slideE = slideWidth;

        //init ba
        for (int i = 0; i < s1.length(); i++) {
            ba[s1.charAt(i) - 'a']++;
        }

        //init sideArray
        for (int i = 0; i < s1.length(); i++) {
            slideArray[s2.charAt(i) - 'a']++;
        }

        if (isEqual(ba,slideArray)) {
            return true;
        }

        while (slideE < s2.length()) {
            slideArray[s2.charAt(slideS) - 'a']--;
            slideArray[s2.charAt(slideE) - 'a']++;
            //iteration
            slideS++;
            slideE++;
            if (isEqual(ba,slideArray)) {
                return true;
            }
        }
        return false;
    }

    public boolean isEqual(int[] a,int[] b) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) {
                return false;
            }
        }
        return true;
    }
```

