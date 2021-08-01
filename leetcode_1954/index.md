# Leetcode_1954 Minimum Garden Perimeter to Collect Enough Apples


Use **binary-search** to solve Leetcode_1954 Minimum Garden Perimeter to Collect Enough Apples
<!--more-->

```python
class Solution:
    def minimumPerimeter(self, n: int) -> int:
        
        
        def getNumber(x):
            t = (1 + x) * x // 2
            return ((x + 1) * t + (x) * t) * 4
        
        l = 1
        r = 31622776 # sqrt(1e15)
        while(l < r):
            mid = (l + r) // 2
            if(getNumber(mid) >= n):
                r = mid
            else:
                l = mid + 1
        
        
        return l * 4 * 2
```
