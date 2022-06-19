---
title: LeetCode 實作解說系列-Two Sum
description: LeetCode-Two Sum
date: 2022-06-18
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
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

### 翻譯

給一個整數陣列nums以及一個整數target，回傳出兩個整數相加等於target在nums裡面的索引值，每個數不能被重複使用，而且只會有一個解。

Example 1:
```json
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
Example 2:
```json
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
Example 3:
```json
Input: nums = [3,3], target = 6
Output: [0,1]
```

Constraints:
* 2 <= nums.length <= 104
* -109 <= nums[i] <= 109
* -109 <= target <= 109
* Only one valid answer exists.
## 解題策略

跑過整個陣列後必定能找到兩兩相加為target的值，用雙層迴圈跑完陣列中的所有數並兩兩相加，方得解答。



## JS程式碼

```js
var twoSum = function(nums, target) {
    for(let i = 0;i<nums.length-1;i++){
        let x = nums[i];
        for(let j = i+1;j<nums.length;j++)
            {
            let  y = nums[j];
            if(x+y===target){
                return [i,j]
            }
            }
 
    }
};
```
