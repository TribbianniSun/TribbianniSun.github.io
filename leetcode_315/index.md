# Leetcode_315



Use **Segment Tree** to solve Leetcode 315 - Count of Smaller Numbers After Self. 
<!--more-->


## Problem Description [Leetcode 315](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)
<p>
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].
</p>



## Examples Test Cases [Leetcode 315](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)


<br>
Example1:
<br>


```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

## Problem Solution [Leetcode 315](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)


```python
import random
from collections import deque, Counter
import math
import functools
import bisect
from typing import List
import heapq


class SegmentTreeNode(object):
    # range[min, max]
    def __init__(self, min, max):
        self.min = min
        self.max = max
        self.mid = (self.max - self.min) // 2 + self.min
        self.count = 0
        self.right = None
        self.left = None
    
    
class SegmentTree(object):
    def __init__(self, root):
        self.root = root

    def update(self, value):
        self.updateHelper(value, self.root)

    def updateHelper(self, value, node):
        if node == None:
            return
        if value < node.min or value > node.max:
            return 
        node.count += 1
        if node.min == node.max:
            return

        working_mid = node.mid
        if node.left == None:
            node.left = SegmentTreeNode(node.min, working_mid)
        
        if node.right == None:
            node.right = SegmentTreeNode(working_mid + 1, node.max)
        
        if value > working_mid:
            self.updateHelper(value, node.right)
        else:
            self.updateHelper(value, node.left)

    def queryRange(self, value):
        return self.queryRangeHelper(value, self.root)

    def queryRangeHelper(self, value, node):
        if node == None:
            return 0
        if value >= node.max:
            return node.count
        
        working_mid = node.mid
        
        if value <= working_mid:
            return self.queryRangeHelper(value, node.left)
        
        else:
            return self.queryRangeHelper(value, node.right) + self.queryRangeHelper(value, node.left)
    

class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        if len(nums) == 0:
            return []
        ret = []
        root = SegmentTreeNode(min(nums), max(nums))
        tree = SegmentTree(root)
        for i in range(len(nums) - 1, -1, -1):
            ret.append(tree.queryRange(nums[i] - 1))
            tree.update(nums[i])
        return ret[::-1]
        
```



## Problem Remark 
- For each TreeNode, **count** refers to how many number between **[max, min]**
- O(nlogk) solution, where k is the max difference
