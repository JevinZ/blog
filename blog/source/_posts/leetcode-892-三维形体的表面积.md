---
title: leetcode-892-三维形体的表面积
catalog: true
date: 2021-10-03 23:35:01
subtitle:
header-img:
tags: [刷题,数学专题,easy]
categories: 刷题
---

### 1.题目描述

给你一个 n * n 的网格 grid ，上面放置着一些 1 x 1 x 1 的正方体。

每个值 v = grid[i][j] 表示 v 个正方体叠放在对应单元格 (i, j) 上。

放置好正方体后，任何直接相邻的正方体都会互相粘在一起，形成一些不规则的三维形体。

请你返回最终这些形体的总表面积。

注意：每个形体的底面也需要计入表面积中。

链接：https://leetcode-cn.com/problems/surface-area-of-3d-shapes

### 2.解题思路  

先计算每个柱体的表面积，柱体表面积等于上下底面面积加高度决定的侧面积

相邻柱体间损失的表面积取决于两柱体中较低的高度

### 3.代码
```cpp
class Solution {
public:
    int surfaceArea(vector<vector<int>>& grid) {
        int n = grid.size();
        int res = 0;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j]>0){
                    res = res + 2 + 4 * grid[i][j];
                    res -= i>0?min(grid[i-1][j],grid[i][j])*2:0;
                    res -= j>0?min(grid[i][j-1],grid[i][j])*2:0;
                }
            }
        }
        return res;
    }
};
```
