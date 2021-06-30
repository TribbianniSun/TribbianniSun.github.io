# Leetcode_827 Making A Large Island



Use **union-find** to solve Leetcode 827 - Making A Large Island. 
<!--more-->

## Problem Description [Leetcode 547](https://leetcode.com/problems/number-of-provinces/)

<p>
In a 2D grid of 0s and 1s, we change at most one 0 to a 1.

After, what is the size of the largest island? (An island is a 4-directionally connected group of 1s).
</p>


## Examples Test Cases [Leetcode 547](https://leetcode.com/problems/number-of-provinces/) 
<br>
Example1:
<br>


```
Input: [[1, 0], [0, 1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
```

<br>
Example2:
<br>


```
Input: [[1, 1], [1, 0]]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger, only one island with area = 4.
```


<br>
Example3:
<br>


```
Input: [[1, 1], [1, 1]]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.
```

## Problem Solution [Leetcode 547](https://leetcode.com/problems/number-of-provinces/) 

```python
import random
from collections import deque, Counter
import math
import functools
import bisect
from typing import List
import heapq

class UnionFind(object):
    def __init__(self):
        self.num_sets = 0
        self.parents = {}
        self.sizes = {}


    def contains(self, p):
        return p in self.parents
    

    def insert(self, p):
        if self.contains(p):
            return

        else:
            self.parents[p] = p
            self.sizes[p] = 1
            self.num_sets += 1
    
    def find(self, p):
        if p != self.parents[p]:
            self.parents[p] = self.find(self.parents[p])
            p = self.parents[p]
        return p

    def union(self, p, q):
        root_p, root_q = map(self.find, (p, q))
        
        # redundant edge
        if root_p == root_q:
            return True
        
        else:
            small, large = sorted([root_p, root_q], key = lambda t : self.sizes[t])
            self.parents[small] = large
            self.sizes[large] += self.sizes[small]
            self.num_sets -= 1
            return False

class Solution:
    def largestIsland(self, grid: List[List[int]]) -> int:
        

        
        dirs = [0, 1, 0, -1, 0]
        # Step1, union 1's and find 0's
        disjoint_set = UnionFind()
        all_zeros = set()
        ret = 0
        m, n = len(grid), len(grid[0])
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 1:
                    base = i * n + j
                    disjoint_set.insert(base)
                    for t in range(len(dirs) - 1):
                        if i + dirs[t] >= 0 and i + dirs[t] < m and j + dirs[t + 1] >= 0 and j + dirs[t + 1] < n and grid[i + dirs[t]][j + dirs[t + 1]] == 1:
                            neighbour = (i + dirs[t]) * n + (j + dirs[t + 1])
                            disjoint_set.insert(neighbour)
                            disjoint_set.union(neighbour, base)
                else:
                    all_zeros.add((i, j))
        
        # edge case, all 1's, just return the size of the grid
        if len(all_zeros) == 0:
            return m * n

        # for all possible zeros, try to flip it
        for zero in all_zeros:
            i, j = zero[0], zero[1]
            leader_size = {}
            for t in range(len(dirs) - 1):
                if i + dirs[t] >= 0 and i + dirs[t] < m and j + dirs[t + 1] >= 0 and j + dirs[t + 1] < n and grid[i + dirs[t]][j + dirs[t + 1]] == 1:
                    leader = disjoint_set.find((i + dirs[t]) * n + (j + dirs[t + 1]))
                    if leader in leader_size:
                        continue
                    else:
                        leader_size[leader] = disjoint_set.sizes[leader]
            ret = max(ret, sum(list(leader_size.values())) + 1)

        return ret
```

## Problem Remark 
- Naive Approach tries all the zeros, and recompute the connected component
- union-find helps us to find the size of the connected component without computing the graph again, O(n*m)
