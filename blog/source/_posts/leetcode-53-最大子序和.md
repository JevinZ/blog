---
title: leetcode_53.最大子序和
catalog: true
date: 2021-09-28 21:08:01
subtitle:
header-img:
tags: [刷题,动态规划,easy]
categories: 刷题
---

### 1.题目描述
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例 1：
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
### 2.解题思路
题目与198.打家劫舍类似，使用dp方程：
```c
nums[i] = max(nums[i],nums[i]+nums[i-1])
```
即可在O(n)时间复杂度内完成题解，不再赘述。
### 3.代码
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = INT_MIN;
        if(nums.size()==1) return nums[0];
        for(int i = 0; i < nums.size(); i++){
            if(i!=0) nums[i] = max(nums[i],nums[i]+nums[i-1]);
            res = max(res,nums[i]);
        }
        return res;
    }
};
```
