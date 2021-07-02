# Leetcode_658 Find K Closest Elements


New **binary-search** to solve Leetcode 658 - Find K Closest Elements.
<!--more-->




## Problem Solution [Leetcode 658](https://leetcode.com/problems/find-k-closest-elements/)

```python
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        # Initialize binary search bounds
        l = 0
        r = len(arr) - k
        while l < r:
            mid = (l + r) // 2
            if x > (arr[mid] + arr[mid + k]) / 2
                l = mid + 1
            else:
                r = mid
        return arr[l:l+k]
                
```
