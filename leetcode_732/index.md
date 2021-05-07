# Leetcode_732 My Calendar III


Use **Segment Tree** to solve Leetcode 732 - My Calendar III. 
<!--more-->

## Problem Description [Leetcode 732](https://leetcode.com/problems/my-calendar-iii/)
<p>

A k-booking happens when k events have some non-empty intersection (i.e., there is some time that is common to all k events.)

You are given some events [start, end), after each given event, return an integer k representing the maximum k-booking between all the previous events.
</p>

Implement the MyCalendarThree class:

- MyCalendarThree() Initializes the object.
- int book(int start, int end) Returns an integer k representing the largest integer such that there exists a k-booking in the calendar.



## Examples Test Cases [Leetcode 732](https://leetcode.com/problems/my-calendar-iii/)
<br>
Example1:
<br>

```
Input
["MyCalendarThree", "book", "book", "book", "book", "book", "book"]
[[], [10, 20], [50, 60], [10, 40], [5, 15], [5, 10], [25, 55]]
Output
[null, 1, 1, 2, 3, 3, 3]

Explanation
MyCalendarThree myCalendarThree = new MyCalendarThree();
myCalendarThree.book(10, 20); // return 1, The first event can be booked and is disjoint, so the maximum k-booking is a 1-booking.
myCalendarThree.book(50, 60); // return 1, The second event can be booked and is disjoint, so the maximum k-booking is a 1-booking.
myCalendarThree.book(10, 40); // return 2, The third event [10, 40) intersects the first event, and the maximum k-booking is a 2-booking.
myCalendarThree.book(5, 15); // return 3, The remaining events cause the maximum K-booking to be only a 3-booking.
myCalendarThree.book(5, 10); // return 3
myCalendarThree.book(25, 55); // return 3
```


## Problem Solution [Leetcode 732](https://leetcode.com/problems/my-calendar-iii/)
```python
import random
from collections import deque, Counter
import math
import functools
import bisect
from typing import List
import heapq

class TreeNode:
    # segment tree with lazy propogation for range max query
    # half-open interval [lo, hi)
    def __init__(self, low, high, val=0, lazy=0, leftChild = None, rightChild = None):
        self.low = low
        self.high = high
        # range max 
        self.val = val
        # bookings to add to the children the next time children get visited
        self.lazy = lazy
        self.leftChild = leftChild
        self.rightChild = rightChild
        
class MyCalendarThree:

    
    MIN_BOUND = 0
    MAX_BOUND = 1e9 + 1
    
    def __init__(self):
        self.root = TreeNode(MyCalendarThree.MIN_BOUND, MyCalendarThree.MAX_BOUND)
        
    def book(self, start: int, end: int) -> int:

        # update the segment from top to down, using lazy propogation
        self.update(self.root, start, end)
        return self.root.val

    
    def update(self, node, start, end):
        

        # we found the match, increment the value and lazy to be propogated
        if node.low == start and node.high == end:
            node.val += 1
            node.lazy += 1
            return


        mid = (node.high - node.low) // 2 + node.low


        # top-down building the segment tree
        if node.leftChild == None and node.rightChild == None:
            node.leftChild = TreeNode(node.low, mid, node.lazy, node.lazy)
            node.rightChild = TreeNode(mid, node.high, node.lazy, node.lazy)
        else:
            node.leftChild.val += node.lazy
            node.leftChild.lazy += node.lazy
            node.rightChild.val += node.lazy
            node.rightChild.lazy += node.lazy
        
        node.lazy = 0
        # after building the children, we are able to traverse downwards
        if mid >= end:
            self.update(node.leftChild, start, end)
        elif mid <= start: 
            self.update(node.rightChild, start, end) 
        else:
            self.update(node.leftChild, start, mid)
            self.update(node.rightChild, mid, end) 

        node.val = max(node.leftChild.val, node.rightChild.val)
        
        return
# credit to https://leetcode.com/problems/my-calendar-iii/discuss/1023625/Python-Segment-Tree-with-Lazy-Propagation
```


## Problem Remark 
- We treat this problem as segment tree(interval tree) where each book would trigger the building of tree
- To build the tree top-down, we utilize **Lazy Propagation**
