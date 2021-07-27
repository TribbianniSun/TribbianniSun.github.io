# Leetcode_18 4sum




Use **data-structure** to solve Leetcode 51 - N-Queens.
<!--more-->

## Problem Solution [Leetcode 18. 4Sum](https://leetcode.com/problems/4sum/)

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        
        dict1 = {}
        ret = set()
        
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                s = nums[i] + nums[j]
                if s in dict1:
                    dict1[s].append([i, j])
                else:
                    dict1[s] = [[i, j]]
        
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                s = nums[i] + nums[j]
                t = target - s
                if t in dict1:
                    for r in dict1[t]:
                        if i not in r and j not in r:
                            c = sorted([nums[i], nums[j], nums[r[0]], nums[r[1]]])
                            ret.add((c[0], c[1], c[2], c[3]))
                            
        return [list(r) for r in ret]
        
        
```
