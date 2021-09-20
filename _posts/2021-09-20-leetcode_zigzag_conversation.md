--- 
title: "[LeetCode] ZigZag Conversation"
excerpt: 지그재그로 글자 배열하기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-zigzag-conversation">](https://leetcode.com/problems/zigzag-conversion/)
*이미지를 클릭하면 문제로 이동합니다.*

이 문제는 직관적이었습니다. 지그재그로 문자열을 배치하면 되는데 for 문을 돌면서 글자를 해당하는 line에 붙여주면 간단하게 풀 수 있습니다. 특히 python같은 경우는 문자를 더하면 자동으로 문자열로 붙여주기 때문에 더욱 쉽게 풀 수 있습니다.

하나 주의할 것은 문자열의 길이가 요구하는 지그재그 라인 수 보다 짧은 경우 입력한 문자열을 그대로 반환하는 것을 예외처리 해주면 시간을 많이 단축할 수 있습니다. 

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if (numRows == 1) | (numRows >= len(s)):
            return s
        lst = [''] * numRows
        cur = 0
        delta = 1
        for i in s:
            if (cur >= numRows-1):
                delta = -1
            elif (cur <= 0):
                delta = 1
            lst[cur] += i
            cur = cur + delta
        ans = "".join(lst)
        return ans
```