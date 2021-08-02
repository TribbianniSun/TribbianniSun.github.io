# Leetcode_1381 Design a Stack With Increment Operation


Use **data-structure** to solve Leetcode 1381 Design a Stack With Increment Operation.
<!--more-->


## Problem Solution [Leetcode 1381. Design a Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation/)


```python
class CustomStack:

    def __init__(self, maxSize: int):
        self.maxSize = maxSize
        self.myStack = []
        self.incrementHistory = [0 for _ in range(maxSize * 4)]    

    def push(self, x: int) -> None:
        if(len(self.myStack) >= self.maxSize):
            return
        else:
            self.myStack.append(x)

    def pop(self) -> int:
        if(len(self.myStack) == 0):
            return -1
        else:
            val = self.myStack[-1]
            l = len(self.myStack)
            val += self.incrementHistory[l]
            self.incrementHistory[l - 1] += self.incrementHistory[l]
            self.incrementHistory[l] = 0
            self.myStack.pop()
            return val

    def increment(self, k: int, val: int) -> None:
        i = min(k, len(self.myStack))
        self.incrementHistory[i] += val
        
```
