# Leetcode_295 Find Median from Data Stream



Use **data-structure, sorted-list** to solve Leetcode 791. Custom Sort String
<!--more-->



## Problem Solution [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)


### Practice How to use sorted list

```python
from sortedcontainers import SortedList
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.sl = SortedList()
        

    def addNum(self, num: int) -> None:
        self.sl.add(num)

    def findMedian(self) -> float:
        l = len(self.sl)
        if l % 2 == 0:
            return (self.sl[l//2] + self.sl[l//2-1]) / 2
        else:
            return self.sl[l//2]


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```
