# Leetcode_1952 Three Divisors


Use **math** to solve Leetcode_1952 Three Divisors
<!--more-->


```python
class Solution:
    def isThree(self, n: int) -> bool:
        ret = 0
        for i in range(1, n + 1):
            if n % i == 0:
                ret += 1
            if ret > 3:
                return False
        return ret == 3
```
