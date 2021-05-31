--- 
title: "[LeetCode] Longest Substring without Repeating Characters"
excerpt: Longest Substring 찾기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-longest-substring-without-repeating-characters">](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
*이미지를 클릭하면 문제로 이동합니다.*

이 문제는 단순하게 풀었다가 통과는 했지만 생각보다 느려서 다시 풀어보았습니다. 먼저 단순하게 푼 버전을 설명하고 개선시킨 코드를 알려드리겠습니다. 개선시킨 코드만 보고싶으신 분은 아래로 이동해 주세요

## 단순하게 푼 버전

먼저 시작하는 지점을 start로 표시해줍니다. 그 다음 checkList을 만들어서 현재 위치에 있는 문자가 이미 있는지 없는지 체크해 준 후 없는 경우 length를 + 1 해주고 체크해준 후 다음 문자로 넘어가서 탐색을 진행합니다. 하지만 이미 체크되어 있는 경우 현재 위치하고 있는 곳의 문자가 체크 해제될 때까지 start를 + 1 해주고 length는 - 1 해줍니다.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        checkList = {}
        maxLen = 0
        length = 0
        start = 0
        for w in s:
            while (checkList.get(w) == 1) :
                checkList[s[start]] = 0
                start += 1
                length -= 1
            checkList[w] = 1
            length += 1
            if length > maxLen :
                maxLen = length
        return maxLen
```

## 개선시킨 버전

개선시킨 버전에서 checkList는 조금 다른 의미를 갖고 있습니다. 개선 시킨 버전에서 checkList는 해당 문자가 마지막으로 등장한 위치를 기록합니다. 마찬가지로 길이를 측정하는 시작점이 되는 start를 갖고 있습니다. 다만 여기서는 이미 체크 되어있는 문자를 해제하기 위해서 하나하나 확인해보는 것이 아닌 해당 문자의 위치가 start를 기점으로 앞에 있는지 뒤에 있는지만 체크해줍니다. start전에 등장한 것이라면 이미 상관 없는 문자기 때문에 다시 등장해도 괜찮지만 start후에 등장한 문자가 또 등장한 것이라면 start위치를 그 문자가 등장한 위치보다 + 1 해줘서 그 사이 값들을 일일히 탐색팔 필요가 없게 해줍니다. 이렇게 하면 시간이 반으로 줄어듭니다.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        checkList = {}
        start = 0
        maxLen = 0
        for cur, letter in enumerate(s):
            if letter not in checkList or checkList[letter] < start :
                maxLen = max(maxLen, cur - start + 1)
            else :
                start = checkList[letter] + 1
            checkList[letter] = cur
        return maxLen
```