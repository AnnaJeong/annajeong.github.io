--- 
title: "[LeetCode] Container With Most Water"
excerpt: 컨데이너에 물 많이 채우기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-container-with-most-water">](https://leetcode.com/problems/container-with-most-water/)
*이미지를 클릭하면 문제로 이동합니다.*

Brute Force로 모든 조합을 다 살펴보게 된다면 O(n2)의 시간이 걸리게 됩니다. 시간을 더 줄이기 위해서는 two pointer 방법으로 접근하면 됩니다.

포인터 하나는 리스트의 시작 부분, 하나는 리스트의 끝 부분에 위치시켜 둘 중 길이가 작은 포인터의 위치를 변경시켜 두 포인터가 곂치지 않을때까지 움직이며 가장 큰 넓이를 찾으면 O(n)으로 시간을 줄일 수 있습니다. 둘 중 길이가 더 작은 포인터를 움직이는 이유는 최종 길이는 길이가 더 작은 포인터가 결정하기 때문입니다. 길이가 더 작은 포인터를 움직이면 다음 높이가 더 높을 경우 너비는 한칸 줄어들지만 높이는 증가할 가능성이 있습니다. 반면에 길이가 더 긴 포인터를 움직이게 되면 현재 높이보다 더 높아질 가능성은 없습니다. 

Two pointer 문제인것을 알면서 이걸 바로 떠올리지 못했다니... 조금 더 수련해야될 것 같네요ㅠ

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        i = 0
        j = len(height)-1
        maxArea = 0
        while (i < j):
            curArea = min(height[i], height[j]) * (j-i)
            if curArea > maxArea :
                maxArea = curArea
            if height[i] < height[j] :
                i += 1
            else :
                j -= 1
        return maxArea
```