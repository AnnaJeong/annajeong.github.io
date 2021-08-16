--- 
title: "[LeetCode] Longest Palindromic Substring"
excerpt: 가장 긴 부분 palindrome 찾기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-longest-palindromic-substring">](https://leetcode.com/problems/longest-palindromic-substring/)
*이미지를 클릭하면 문제로 이동합니다.*

이 문제는 푸는데 애를먹었죠ㅠㅠ 아직 알고리즘 수련이 한참 부족하다는 것을 느끼고 더 열심히 해야겠다고 마음을 먹었습니다.

단순하게 완탐을 해서 풀 수도 있지만 그렇게 푼다면 시간초과에 걸리고 마는 문제입니다.
시간을 줄이기 위해 한번 계산했던 결과를 재사용하는 Dynamic Programming 방법을 사용해서 풀어보았습니다.

## Palindrome 이란?
먼저 palindrome이란 대칭이 되는 문자열을 말합니다. 예를들면 제 이름인 Anna도 앞에서부터 쓰나 뒤에서부터 쓰나 스펠링이 같이 때문에 palindrome입니다. 이 문제는 하나의 문자열내에서 가장 긴 부분 palindrome을 찾는 문제입니다.

## 문제 풀이
### DP 적용하기
결과를 어떻게 재사용할 수 있을까요? 먼저 palindrome이란 문자열이 대칭이 되는 것이기 때문에 palindrome내의 부분 문자열도 대칭인 palindrome이 될 수 밖에 없습니다. 이를 그림으로 표현하면 다음과 같습니다.
![graph1](../../assets/images/algorithm/leetcode-longest-palindromic-substring-1)
참 쉽죠? 우리의 역할은 이거를 코드화 하는 것 뿐입니다. 하지만 이렇게 쉬웠다면 제가 머리를 싸매고 고민할 필요가 없었겠죠?

### 부분 palindrome 찾기
위의 경우는 문자열 자체가 완벽한 palindrome이기 때문에 이런 방법으로 풀 수 있었겠지만 부분 palindrome은 어떻게 찾을 수 있을까요?

말 그대로 부분부분으로 나눠서 보면 됩니다.
![graph2](../../assets/images/algorithm/leetcode-longest-palindromic-substring-2)
위의 표에서 row는 문자열이 시작하는 부분을 column은 문자열이 끝나는 부분을 나타낸다고 보면 모든 부분문자열에 대해서 검사를 해볼 수 있습니다. 그렇다면 여기서 어떻게 하면 결과를 재사용할 수 있을까요? 답은 간단합니다. 시작 문자와 끝나는 문자가 같은 경우에 바로 전 까지의 부분 palindrome이 존재했다면 바로 전 까지의 부분 palidrome의 결과 + 2를 해주면 됩니다. 말로 하면 어려우니 코드로 한번 작성해보겠습니다.
```python
# s는 문자열, i가 row, j가 column일 때
if s[i] == s[j] & dp[i+1][j-1] != 0:
    dp[i][j] = dp[i+1][j-1] + 2
```
표도 한번 채워볼까요?
![graph3](../../assets/images/algorithm/leetcode-longest-palindromic-substring-3)
어때요 참 쉽죠?

하지만 마지막으로 하나 더 고려해줘야 할 사항이 있습니다. 이 로직으로 찾는 경우 aa혹은 bb와 같이 연속된 2글자 짜리의 palindrome은 고려가 되지 않습니다. 따라서 마지막으로 s[i]=s[j]이고 start-end=1인 경우만 추가적으로 고려해준다면 문제풀이는 끝입니다.

휴 뿌듯하네요. 다음에는 더 업그레이된 모습으로 돌아오겠습니다. 오늘도 keep going!
``` python
class Solution:
    def makeArray(self, len):
        arr = []
        for i in range(len):
            tmp = [0] * len
            tmp[i] = 1
            arr.append(tmp)
        return arr
    def longestPalindrome(self, s: str) -> str:
        arr = self.makeArray(len(s))
        ansLen = 0
        x = 0
        y = 0
        for i in range(len(s)-1, -1, -1):
            for j in range(i+1, len(s)):
                if (s[i] == s[j]):
                    if (arr[i+1][j-1] == 0) & (i + 1 != j):
                        continue
                    arr[i][j] = arr[i+1][j-1]+2
                    if (arr[i][j] > ansLen) :
                        ansLen = arr[i][j]
                        x = i
                        y = j
        return s[x:y+1]
```

