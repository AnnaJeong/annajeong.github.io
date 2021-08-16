--- 
title: "[LeetCode] Add Two Numbers"
excerpt: 링크드 리스트의 숫자 두 개 더하기

categories:
    - Algorithm
tags:
    - LeetCode
    - python
use_math: true
toc: true
toc_sticky: true
---

[<img src="../../assets/images/algorithm/leetcode-add-two-numbers">](https://leetcode.com/problems/add-two-numbers/)
*이미지를 클릭하면 문제로 이동합니다.*

python으로 처음 알고리즘 문제를 풀어봤다는 점을 빼고는 상당히 쉬운 문제였습니다. Linked List에는 숫자가 역순으로 한 자씩 저장되어 있고 두 개의 Linked List의 값들을 더해서 결과물을 마찬가지로 Linked List로 반환하는 문제입니다.

두 가지 방법을 생각했는데 하나는 말 그대로 한칸 한칸씩 더하면서 10이 넘는 값을 다음 칸으로 올려주는 방식으로 푸는 것이고 다른 하나는 Linked List의 숫자를 10진수로 변환해서 푸는 방법입니다. 저는 전자로 풀었습니다.

리본적으로 Linked List 구조체는 주어지기 때문에 참고용으로 주석처리 되어있어서 만들 필요도 없습니다. 참 쉽죠?

반환할때 정답 Linked List의 시작하는 노드를 반환하는 것만 기억하면 쉽게 풀립니다. 이것때매 조금 헤맸네요. 앞으로는 c나 c++말고 파이썬으로 알고리즘 푸는 연습도 더 많이 해야될 것 같습니다.

문제가 쉬워서 별로 쓸말이 없어서 주절주절 말했네요. 코드 첨부하고 마치도록 하겠습니다.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        ans = cur = ListNode(0)
        buf = 0
        val = 0
        while(l1 or l2):
            if (l1) :
                val += l1.val
                l1 = l1.next
            if (l2) :
                val += l2.val
                l2 = l2.next
            val += buf
            buf = val // 10
            cur.next = ListNode(val % 10)
            val = 0
            
            cur = cur.next
            
        if buf != 0:
            cur.next = ListNode(buf)
        return ans.next
```