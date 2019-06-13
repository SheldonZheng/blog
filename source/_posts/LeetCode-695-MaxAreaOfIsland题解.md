---
title: LeetCode.695.MaxAreaOfIsland题解
date: 2019-06-13 16:45:22
categories: LeetCode
tags:
- LeetCode
---



## LeetCode 695 Max Area of Island 岛屿的最大面积题解



## Description:

Given a non-empty 2D array `grid` of 0's and 1's, an **island** is a group of `1`'s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

**Example 1:**

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return 

```
6
```

. Note the answer is not 11, because the island must be connected 4-directionally.

**Example 2:**

```
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return 

```
0
```

.

**Note:** The length of each dimension in the given `grid` does not exceed 50.



## 题解:

从头开始遍历每一个是1的地方，然后递归地遍历这个1的四周，要注意边界条件，遍历过的设置成0避免重复遍历



## Code:

```java
public int maxAreaOfIsland(int[][] grid) {
        if (grid == null) {
            return 0;
        }
        int r = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    int num = search(grid, i, j);
                    r = Math.max(r, num);
                }
            }
        }
        return r;
    }

    public int search(int[][] grid,int i,int j) {
        if (i >= 0 && i < grid.length && j >= 0 && j < grid[i].length && grid[i][j] == 1) {
            //no repeat
            grid[i][j] = 0;
            int num = 1 + search(grid,i + 1,j) + search(grid , i - 1,j) + search(grid,i,j + 1) + search(grid,i, j - 1);
            return num;
        } else {
            return 0;
        }
    }
```

