---
layout: post
title:  "LeetCode - Palindrome Number"
summary: 릿코드 문제풀이 포스팅
author: 서준석
date: '2020-08-19 15:13:00 +0530'
category: algorithm
thumbnail: /assets/img/leetcode/palindromenumber.png
keywords: algorithm, leetcode, easy problem
permalink: /blog/leetcode-palindromenumber
---
# Reverse Integer

## 1. 문제
>Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.<br/>
Coud you solve it without converting the integer to a string<br/>



### 2. 해결법
1. 정수형의 문자열형식 변환 없이 문제 palindrome 문제 풀기
2. 음수는 false 리턴
3. reverse 정수 만든 후 비교

### 3. 실패 사유
1. 실행 시간이 128ms로 하위 권으로 나옴
   * 다른 풀이들은 str()을 사용(???)

### 4. 코드
1. str 사용 코드

|실행시간|메모리사용률|
|:---|:---|
|<center>80ms</center>|<center>13.6 MB</center>|

```python
class Solution:    
    def isPalindrome(self, x: int) -> bool:
        if x<0:
            return False
        
        return x==int(str(x)[::-1])
```

2. str 미사용 코드

|실행시간|메모리사용률|
|:---|:---|
|<center>128ms</center>|<center>14.1 MB</center>|

```python
class Solution:
    def reverseInteger(self, x: int) -> int:
        intList = []
        cnt = 0
            
        while x >= 10:
            intList.append(x%10)
            x//=10
            cnt+=1
            
        intList.append(x%10)
        x = 0
        
        for i in intList:
            x+=i*(10**cnt)
            cnt-=1
        
        return x
    
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False
        
        res = self.reverseInteger(x)
         
        if res == x:
            return True
        else:
            return False
```

### 5. 결과
str을 통해 int형 정수를 문자열형으로 변환할 경우 실행 시간이 감소했다.<br/>
하지만 Follow up에서 "Coud you solve it without converting the integer to a string?"<br/>
라고 했기 때문에 나는 **형변환**을 쓰지 않은 방법을 내 결과로 생각한다.<br/>
