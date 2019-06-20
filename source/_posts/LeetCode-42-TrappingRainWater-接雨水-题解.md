---
title: LeetCode.42.TrappingRainWater.接雨水.题解
date: 2019-06-20 17:25:28
categories:
- LeetCode题解
tags:
- LeetCode
---

[原题地址](https://leetcode.com/problems/trapping-rain-water/)



## Description:

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```



## 题解:

用栈来解，当遇到栈为空或者当前高度小于栈顶存的高度的时候，当前高度压入栈；

当遇到当前高度高于栈顶高度时，先pop一个作为底，然后当前的栈顶就是左边的最高高度，当前高度就是右边的最高高度，刚才pop出去的那个就是底的高度，这时候底一定是平的。。。思考一下；

然后就能算出来面积，加一起就好；



## Code:

```java
class Solution {
    public int trap(int[] height) {
        int count = 0;
        if (height == null || height.length < 2) {
            return count;
        }
        Stack<Integer> stack = new Stack<>();
        int i = 0;
        while (i < height.length){
            if (stack.empty() || height[i] <= height[stack.peek()]) {
                stack.push(i++);
            }
            else {
                int j = stack.pop();
                if (stack.isEmpty()) {
                    continue;
                }
                int r =  (Math.min(height[i],height[stack.peek()]) - height[j])  * (i - stack.peek() - 1);
                count += r;
            }
        }
        return count;
    }
}
```

