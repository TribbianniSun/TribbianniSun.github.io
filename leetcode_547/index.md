# Leetcode_547 Number of Provinces



Use **Union Find** to solve Leetcode 547 - Number of Provinces. 
<!--more-->

## Problem Description [Leetcode 547](https://leetcode.com/problems/number-of-provinces/)

<p>
There are n cities. Some of them are connected, while some are not. If city <strong>a</strong> is connected directly with city <strong>b</strong>, and city <strong>b</strong> is connected directly with city <strong>c</strong>, then city <strong>a</strong> is connected indirectly with city <strong>c</strong>. 

A province is a group of directly or indirectly connected cities and no other cities outside of the group.
You are given an n x n matrix isConnected where <em>isConnected[i][j] = 1</em> if the ith city and the jth city are directly connected, and <em>isConnected[i][j] = 0</em> otherwise.

Return the total number of provinces.
</p>


## Examples Test Cases [Leetcode 547](https://leetcode.com/problems/number-of-provinces/) 
<br>
Example1:
<br>
<img src="https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg">

```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2
```

<br>
Example2:
<br>
<img src="https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg">

```
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3
```

## Problem Solution [Leetcode 547](https://leetcode.com/problems/number-of-provinces/) 

```python
import random
from collections import deque
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
        return self.parents[p]


    def union(self, p, q):
        root_p, root_q = self.find(p), self.find(q)
        if root_p == root_q:
            return
        else:

            if self.sizes[root_p] > self.sizes[root_q]:
                small_root = root_q
                large_root = root_p
            else:
                small_root = root_p
                large_root = root_q
            
            self.parents[small_root] = large_root
            self.sizes[large_root] += self.sizes[small_root]
            self.num_sets -= 1
    

class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        disjoint_set = UnionFind()
        n = len(isConnected)
        for i in range(n):
            disjoint_set.insert(i)

        for i in range(n):
            for j in range(n):
                if isConnected[i][j]:
                    disjoint_set.union(i, j)
        return disjoint_set.num_sets
```

## Problem Remark 
- To find the connected component in undirected graph, Union Find(Disjoint Set) is the handy data structure to use.
