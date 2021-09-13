---
layout: post
title:  "LeetCode - Roman to Integer"
summary: 릿코드 문제풀이 포스팅
author: 서준석
date: '2020-08-20 17:54:00 +0530'
category: algorithm
thumbnail: /assets/img/leetcode/romantointeger.png
keywords: algorithm, leetcode, easy problem
permalink: /blog/leetcode-romantointeger
---
# Reverse Integer

## 1. 문제
>Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.<br/>For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.<br/>Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:<br/>
* I can be placed before V (5) and X (10) to make 4 and 9.
* X can be placed before L (50) and C (100) to make 40 and 90. 
* C can be placed before D (500) and M (1000) to make 400 and 900.
>Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.


### 2. 해결법
1. dictionary 사용하여 해당 Key에 맞는 Value를 더하기
2. in 키워드와 list를 활용해 주어진 조건 간단하게 구현하기(IV는 4...) 

### 3. 실패 사유
>첫번째 fail : 주어진 조건을 고려안함


### 4. 코드
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        dic = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        res = 0
        pic = 0        

        while pic != len(s):
            if s[pic] in ['I','X','C']:                
                if s[pic:pic+2] in ['IV','IX','XL','XC','CD','CM']:
                    res+=(dic.get(s[pic+1])-dic.get(s[pic]))
                    pic+=2
                else:
                    res+=dic.get(s[pic])
                    pic+=1
            else:
                res+=dic.get(s[pic])
                pic+=1
                
        
        return res
```

### 5. 결과
![결과1](../assets/img/leetcode/romantointeger_result1.png)
![결과2](../assets/img/leetcode/romantointeger_result2.png)
