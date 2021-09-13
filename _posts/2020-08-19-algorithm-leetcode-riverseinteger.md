---
layout: post
title:  "LeetCode - Reverse Integer"
summary: 릿코드 문제풀이 포스팅
author: 서준석
date: '2020-08-19 02:10:00 +0530'
category: algorithm
thumbnail: /assets/img/leetcode/reverseinteger.png
keywords: algorithm, leetcode, easy problem
permalink: /blog/leetcode-reverseinteger
---
# Reverse Integer

## 1. 문제
>Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.<br/>[ 32bit signed 정수 범위내에서 오직 저장된 정수들만을 다루려 한다. 주어진 문제에서 바뀐 정수가 범위를 넘어설 때 0을 리턴하자. ]


### 2. 해결법
1. O(N) 시간 복잡도로 해결하기
2. sign 변수로 음수 저장 후 반환
3. -2^31 ~ 2^31-1 [-2,147,483,648 ~ 2,147,483,647]

### 3. 실패 사유
>첫번째 fail : 1534236469 라는 수의 TestCase에 의해 실패했다.
해결법 : OutPut의 범위가 integer의 범위 안에 들어오지 못한 경우 0을 return

>두번째 fail : -2,147,483,648의 결과값이 그대로 나옴
해결법 : 음수 후 리턴을 안함...


### 4. 코드
```python
import math
class Solution:
    def reverse(self, x: int) -> int:
        intList = []
        res = 0
        cnt = 0
        sign = 1
        
                
        # x가 0보다 작으면 sign 변수에 음수 저장후 x 양수 전환
        if x < 0:
            sign *= -1
            x*=-1
            
        while x >= 10:
            intList.append(x%10)
            x//=10
            cnt+=1
            
        intList.append(x%10)

        for i in intList:
            res+=i*(10**cnt)
            cnt-=1
        
        if sign < 0:
            res*=sign
        
        # integer의 범위를 넘어서면 0 리턴
        if res >= math.pow(2,31)-1 or res <= -(math.pow(2,31)):
            return 0
        else:
            return res
```

### 5. 결과
![ReverseInteger결과1](../assets/img/leetcode/reverseinteger_result1.png)
![ReverseInteger결과2](../assets/img/leetcode/reverseinteger_result2.png)
![ReverseInteger결과3](../assets/img/leetcode/reverseinteger_result3.png)
