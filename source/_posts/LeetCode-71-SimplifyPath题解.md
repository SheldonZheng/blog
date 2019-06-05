---
title: LeetCode.71.SimplifyPath题解
date: 2019-06-05 18:17:40
categroies:
- LeetCode题解
tags:
- LeetCode
---



## LeetCode 71 Simplify Path 题解

[题目地址](https://leetcode.com/problems/simplify-path/)

### Description:

Given an **absolute path** for a file (Unix-style), simplify it. Or in other words, convert it to the **canonical path**.

In a UNIX-style file system, a period `.` refers to the current directory. Furthermore, a double period `..` moves the directory up a level. For more information, see: [Absolute path vs relative path in Linux/Unix](https://www.linuxnix.com/abslute-path-vs-relative-path-in-linuxunix/)

Note that the returned canonical path must always begin with a slash `/`, and there must be only a single slash `/` between two directory names. The last directory name (if it exists) **must not** end with a trailing `/`. Also, the canonical path must be the **shortest**string representing the absolute path.

 

**Example 1:**

```
Input: "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

**Example 2:**

```
Input: "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

**Example 3:**

```
Input: "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

**Example 4:**

```
Input: "/a/./b/../../c/"
Output: "/c"
```

**Example 5:**

```
Input: "/a/../../b/../c//.//"
Output: "/c"
```

**Example 6:**

```
Input: "/a//b////c/d//././/.."
Output: "/a/b/c"
```



### 题解:

首先想的比较复杂，构造一个结构去存当前目录，然后从前向后扫描字符串，去掉重复的/，需要回退就回退；

看了解法其实用一个栈就可以。。用String的split方法会自动去掉多余的/。。。



### Code:

```java
public String simplifyPath(String path) {
        if (path == null || path.length() == 0) {
            return "";
        }
        //clear
        Deque<String> stack = new LinkedList<>();
        Set<String> skip = new HashSet<>(Arrays.asList("..", ".", ""));

        String[] splited = path.split("/");
        for (int i = 0; i < splited.length; i++) {
            if (splited[i].equals("..") && !stack.isEmpty()) {
                stack.pop();
            } else if (!skip.contains(splited[i])) {
                stack.push(splited[i]);
            }
        }
        if (stack.isEmpty()) {
            return "/";
        }
        String result = "";
        for (String s : stack) {
            result = "/" + s + result;
        }
        return result;
    }
```

