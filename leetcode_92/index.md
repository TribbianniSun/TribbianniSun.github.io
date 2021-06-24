# Leetcode_92 Reverse Linked List II


Use **Data Struccture** to solve Leetcode 792 - Reverse Linked List II.
<!--more-->

## Problem Solution [Leetcode 792](https://leetcode.com/problems/reverse-linked-list-ii/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        dummy = ListNode()
        dummy.next = head
        preNode = dummy
        for i in range(left - 1):
            preNode = preNode.next
        
        workingNode = preNode.next
        nextWorkingNode = workingNode.next
        for i in range(right - left):
            tmp = nextWorkingNode.next
            nextWorkingNode.next = workingNode
            workingNode = nextWorkingNode
            nextWorkingNode = tmp
        
        preNode.next.next = nextWorkingNode
        preNode.next = workingNode
        return dummy.next
            
```


