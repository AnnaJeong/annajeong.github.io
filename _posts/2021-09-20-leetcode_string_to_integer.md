--- 
title: "[LeetCode] String to Integer (atoi)"
excerpt: 문자열을 숫자로 변환하기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-atoi-1">](https://leetcode.com/problems/string-to-integer-atoi/)
[<img src="../../assets/images/algorithm/leetcode-atoi-2">](https://leetcode.com/problems/string-to-integer-atoi/)
*이미지를 클릭하면 문제로 이동합니다.*

c나 c++에서는 문자열을 ascii 코드로 변환할 수 있었지만 python에서는 ord()라는 것을 사용해야 한다는 것 말고는 특별히 여려운 문제는 아니었습니다.
 먼저 앞에 공백을 없애준 후 부호가 있다면 먼저 받아준 뒤 for문을 사용해 탐색을 합니다. 이 때 숫자가 아닌 문자가 나온다면 for문을 끝내고 그 전까지의 결과를 반환합니다. 

 ```python
 class Solution:
    def myAtoi(self, s: str) -> int:
        ans = 0
        s = s.strip() # remove whitespace
        
        if len(s) <= 0 : # if only whitespace exists
            return 0
        
        sign = 1 # decide sign
        if s[0] == '-':
            sign = -1
            s = s[1:]
        elif s[0] == '+' :
            s = s[1:]
            
        for c in s:
            if (ord(c) < ord('0')) | (ord(c) > ord('9')) :
                break
            ans = ans * 10 + (ord(c) - ord('0'))
            if (ans > 2147483648) & (sign == -1)  :
                ans = 2147483648
                break
            elif (ans  > 2147483647) & (sign == 1):
                ans = 2147483647
                break
        ans = ans * sign
        return ans
```