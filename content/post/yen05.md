---
title: LeetCode 實作解說系列-Longest Common Prefix
description: LeetCode-Longest Common Prefix
date: 2022-06-19
categories:
    - LeetCode
    - JavaScript
    - LeetCode Easy
    - 解說
tags : [
    "LeetCode",
]
---

## 題目解說

### 原題目

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

 

**Example 1:**

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

 

**Constraints:**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

### 翻譯

給定一個陣列strs，裡面會有字串，找出此陣列字串相同的前綴，如果沒有，返回`""`。

## 解題策略

邏輯上是後面的字串去跟前面的做比較就好，所以聲明字串`pre`，一開始就宣告為陣列的第一個元素，如果比對不到，就將`pre`刪掉一個字符，刪到比對出相同前綴為止。

## JS程式碼

```js
var longestCommonPrefix = function(strs) {
   if(strs == null || strs.length == 0) return "";
   let pre =strs[0]
   console.log(strs.length)
   for(let i =1;i<strs.length;i++){
       while(strs[i].indexOf(pre) != 0){
           pre=pre.substring(0, pre.length - 1);
       }
   }
    return pre;
};
```