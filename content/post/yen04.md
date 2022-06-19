---
title: LeetCode 實作解說系列-Roman to Integer
description: LeetCode-Roman to Integer
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

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

 

**Example 1:**

```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

**Example 2:**

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 3:**

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

 

**Constraints:**

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

### 翻譯

這題主要是在說羅馬數字的計算方式，並告知`('I', 'V', 'X', 'L', 'C', 'D', 'M')` 分別等於數字多少，且 `4 不是 IIII 而是 VI` ，以此類推應用到 `9,40,90,400,900`。

## 解題策略

解題邏輯是讓每個字母等於一個數字，再用 `object ={key:value}` 的方式加總就好，首先要處理的就是 `4,9,40,90,400,900` ，我宣告的 object 把` 'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900` 用一個字母取代掉 `'f':4,'n':9,'l':40,'c':90,'d':400,'m':900`，接著是做字串s的文字取代 `s.replace('IV','f').replace('IX','n').replace('XL','l').replace('XC','c').replace('CD','d').replace('CM','m')`，最後利用迴圈加上 `charAt()`就可以逐一取值並加總。

## JS程式碼

```js
var romanToInt = function(s) {
    //'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900
    const obj  ={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000,'f':4,'n':9,'l':40,'c':90,'d':400,'m':900};
    let new_s = s.replace('IV','f').replace('IX','n').replace('XL','l').replace('XC','c').replace('CD','d').replace('CM','m')
    let sum = 0
    for(let i = 1;i<=new_s.length;i++){
       sum = sum + obj[new_s.charAt(i-1)]
    }
    return sum;
};
```

