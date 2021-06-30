# Leetcode_1722 Minimize Hamming Distance After Swap Operations


Use **union-find** to solve Leetcode 1722 - Minimize Hamming Distance After Swap Operations.
<!--more-->

## Problem Description [Leetcode 1722](https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/)

<p>
You are given two integer arrays, source and target, both of length n. You are also given an array allowedSwaps where each allowedSwaps[i] = [ai, bi] indicates that you are allowed to swap the elements at index ai and index bi (0-indexed) of array source. Note that you can swap elements at a specific pair of indices multiple times and in any order.

The Hamming distance of two arrays of the same length, source and target, is the number of positions where the elements are different. Formally, it is the number of indices i for 0 <= i <= n-1 where source[i] != target[i] (0-indexed).

Return the minimum Hamming distance of source and target after performing any amount of swap operations on array source.
</p>


## Examples Test Cases [Leetcode 1722](https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/)
<br>


<br>
Example1:
<br>

```
Input: source = [1,2,3,4], target = [2,1,4,5], allowedSwaps = [[0,1],[2,3]]
Output: 1
Explanation: source can be transformed the following way:
- Swap indices 0 and 1: source = [2,1,3,4]
- Swap indices 2 and 3: source = [2,1,4,3]
The Hamming distance of source and target is 1 as they differ in 1 position: index 3.
```


Example1:
<br>

```
Input: source = [1,2,3,4], target = [1,3,2,4], allowedSwaps = []
Output: 2
Explanation: There are no allowed swaps.
The Hamming distance of source and target is 2 as they differ in 2 positions: 
index 1 and index 2.
```

## Problem Solution [Leetcode 1722](https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/)

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
        self.num_sizes = 0
        self.parents = {}
        self.sizes = {}


    def contains(self, p):
        return p in self.parents
    

    def insert(self, p):
        if self.contains(p):
            return 
        else:
            self.num_sizes += 1
            self.parents[p] = p
            self.sizes[p] = 1
    

    def find(self, p):
        if p != self.parents[p]:
            self.parents[p] = self.find(self.parents[p])
            p = self.parents[p]
        return p
    
    def union(self, p, q):
        root_p, root_q = map(self.find, (p, q))

        # this means that we found a redundant edge
        if root_p == root_q:
            return True

        else:
            small, large = sorted([root_p, root_q], key = lambda t: self.sizes[t])
            self.parents[small] = large
            self.sizes[large] += self.sizes[small]
            self.num_sizes -= 1
            return False



class Solution:
    def minimumHammingDistance(self, source: List[int], target: List[int], allowedSwaps: List[List[int]]) -> int:
        disjoint_set = UnionFind()
        n = len(source)
        for i in range(n):
            disjoint_set.insert(i)
        
        # build the union graph
        # in each group, the numbers can be placed anywhere
        for edge in allowedSwaps:
            disjoint_set.union(edge[0], edge[1])
        
        # hashmap, 
        # group leader -> set[indices in that group]
        leader_member = {}
        print(disjoint_set.parents)
        for member, leader in disjoint_set.parents.items():
            # This is the real leader for this member
            leader = disjoint_set.find(member)
            if leader in leader_member:
                leader_member[leader].add(member)
            else:
                leader_member[leader] = set([member])

        print(leader_member)
        ret = 0
        # for all the members, try to figure out the distance
        for members in leader_member.values():
            source_numbers = [source[i] for i in members]
            target_numbers = [target[i] for i in members]
            ret += sum((Counter(source_numbers) - Counter(target_numbers)).values())
        return ret
        
```

## Problem Remark 
- To solve this problem, we need to observe that if (0, 1) is exchangeable and (0, 2) is exchangeable,
then any pair in (0, 1, 2) can be exchangeble.
- The remaining problem is how to detect connected components in the graph -> use union-find.
- Counter, the subclass of dictionary, supports many great opeartions.


