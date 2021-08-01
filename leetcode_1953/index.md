# Leetcode_1953 Maximum Number of Weeks for Which You Can Work


Use **math** to solve Leetcode_1953 Maximum Number of Weeks for Which You Can Work
<!--more-->



```python
class Solution:
    def numberOfWeeks(self, milestones: List[int]) -> int:
        s = sum(milestones)
        m = max(milestones)
        if (m + m > s):
            return 2*(s-m) + 1
        else:
            return s
```
