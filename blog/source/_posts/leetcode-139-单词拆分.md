---
title: leetcode_139.单词拆分
catalog: true
date: 2021-09-28 22:14:44
subtitle:
header-img:
tags: [刷题,动态规划,medium,新知识]
categories: 刷题
---

### 1.新知识！
1.vector的初始化：
```cpp
vector<bool> dp(10, false);//dp初始化为容量为10，默认值为flase的可变长数组
```
2.c++ 利用vector 初始化 hashset
```cpp
vector<string>& wordDict;
unordered_set<string> m(wordDict.start(),wordDict.end());
```
### 2.题目描述
给定一个非空字符串 s 和一个包含非空单词的列表 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。

链接：https://leetcode-cn.com/problems/word-break

示例 1：
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。

示例 2：
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。

### 3.解题思路
因为这周刷的动态规划专题，很自然的往dp上去想，但没有思路。看了一位同学的评论后才有了思路。
简单的表述来说，就是使用dp[i]来描述字符串的前i位能否被Dict中的元素拆分，i从1开始，直到到达所要匹配的字符串长度。
每次循环中，将i拆分成2半，后一半利用Dict中的元素，前一半为剩余部分，查找是否存在：
剩余部分的dp[i]为true并且能够使用Dict来组成当前i长度的字符串的组合，找到则dp[i]为true并开始下一个循环。
注意上一句的描述就是一个状态转移的过程，从较短的i加上匹配的单词变为较长的i，查找过程利用hashset加快查找，但可能内存需求较高。
最后返回dp[s.size()]。

### 4.代码
```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.size()+1,false);
        unordered_set<string> m(wordDict.begin(),wordDict.end());
        int maxlength = 0;
        for(int i = 0; i < wordDict.size(); i++){
            maxlength = max(maxlength,(int)wordDict[i].size());
        }
        dp[0] = true;
        for(int i = 1; i <= s.size(); i++){
            for(int j = max(i-maxlength,0) ; j < i; j++){
                if(dp[j] && m.find(s.substr(j,i-j))!=m.end()){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.size()];
    }
};
```
