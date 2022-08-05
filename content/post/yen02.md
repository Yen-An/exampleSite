---
title: LeetCode 實作解說系列-Palindrome Number
description: LeetCode-Palindrome Number
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

Given an integer `x`, return `true` if `x` is palindrome integer.

An integer is a **palindrome** when it reads the same backward as forward.

For example, `121` is a palindrome while `123` is not.

**Example 1:**

```
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left
```

**Example 2:**

```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Constraints:**

- `-231 <= x <= 231 - 1`

### 翻譯

給定一個整數x，回傳x是不是個相反數。舉例來說121相反為121，回傳true，-121相反為121-，回傳false。

## 解題策略

將x轉為字串xstr，再將xstr利用reverse函數做字序的反轉，最後將x與xstr做一般相等比較。

## JS程式碼

```javascript
var isPalindrome = function(x) {
    let xstr = x.toString().split("").reverse().join("")
    console.log(xstr)
    if(x==xstr){
        return true;
    }
    else{
        return false;
    }
};
```

