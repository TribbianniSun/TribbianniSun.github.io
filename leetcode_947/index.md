# Leetcode_947 Most Stones Removed with Same Row or Column



Use **Union Find** to solve Leetcode 947 - Most Stones Removed with Same Row or Column. 
<!--more-->


## Problem Description [Leetcode 947](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)
<p>
On a 2D plane, we place n stones at some integer coordinate points. Each coordinate point may have at most one stone.

A stone can be removed if it shares either **the same row or the same column** as another stone that has not been removed.

Given an array stones of length n where stones[i] = [xi, yi] represents the location of the ith stone, return the largest possible number of stones that can be removed.
</p>



## Examples Test Cases [Leetcode 947](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)
<br>
Example1:
<br>

```
Input: stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 5
Explanation: One way to remove 5 stones is as follows:
1. Remove stone [2,2] because it shares the same row as [2,1].
2. Remove stone [2,1] because it shares the same column as [0,1].
3. Remove stone [1,2] because it shares the same row as [1,0].
4. Remove stone [1,0] because it shares the same column as [0,0].
5. Remove stone [0,1] because it shares the same row as [0,0].
Stone [0,0] cannot be removed since it does not share a row/column with another stone still on the plane.
```

<br>
Example2:
<br>

```
Input: stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]
Output: 3
Explanation: One way to make 3 moves is as follows:
1. Remove stone [2,2] because it shares the same row as [2,0].
2. Remove stone [2,0] because it shares the same column as [0,0].
3. Remove stone [0,2] because it shares the same row as [0,0].
Stones [0,0] and [1,1] cannot be removed since they do not share a row/column with another stone still on the plane.
```

<br>
Example3:
<br>

```
Input: stones = [[0,0]]
Output: 0
Explanation: [0,0] is the only stone on the plane, so you cannot remove it.
```



## Problem Solution [Leetcode 947](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)


```python
from collections import deque, Counter

class UnionFind(object):
    def __init__(self):
        self.num_sets = 0
        self.parents = {}
        self.sizes = {}

    def contains(self, p):
        return p in self.parents

    def insert(self, p):
        # already inserted
        if p in self.parents:
            return True
        else:
            self.num_sets += 1
            self.parents[p] = p
            self.sizes[p] = 1
            return False

    def find(self, p):
        if p != self.parents[p]:
            self.parents[p] = self.find(self.parents[p])
            p = self.parents[p]
        return p
    
    def union(self, p, q):
        root_p, root_q = map(self.find, [p, q])
        if root_p == root_q:
            return True
        else:
            small, large = sorted([root_p, root_q], key = lambda t: self.sizes[t])
            self.parents[small] = large
            self.sizes[large] += self.sizes[small]
            self.num_sets -= 1

class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:

        row_stone = {} # row -> stone location
        col_stone = {} # col -> stone location
        for stone in stones:
            i, j = stone[0], stone[1]
            location = (i, j)
            if i in row_stone:
                row_stone[i].add(location)
            else:
                row_stone[i] = set()
                row_stone[i].add(location)

            if j in col_stone:
                col_stone[j].add(location)
            else:
                col_stone[j] = set()
                col_stone[j].add(location)

        disjoint_set = UnionFind()
        all_stone = set()
        for stone in stones:
            i, j = stone[0], stone[1]
            location = (i, j)

            if disjoint_set.contains(location):
                continue
            else:
                # do a little bfs here to find all the connected component
                my_queue = deque()
                my_queue.append(location)
                row_seen = set()
                col_seen = set()
                while(len(my_queue) != 0):
                    cur_loc = my_queue.pop()
                    disjoint_set.insert(cur_loc)
                    disjoint_set.union(cur_loc, location)
                    all_stone.add(cur_loc)
                    i, j = cur_loc[0], cur_loc[1]
                    if i not in row_seen:
                        row_seen.add(i)
                        for stone in row_stone[i]:
                            my_queue.append(stone)
                            
                    if j not in col_seen:
                        col_seen.add(j)
                        for stone in col_stone[j]:
                            my_queue.append(stone)

        leader_size = {}
        for stone in all_stone:
            real_leader = disjoint_set.find(stone)
            if real_leader not in leader_size:
                leader_size[real_leader] = disjoint_set.sizes[real_leader]
            else:
                leader_size[real_leader] = disjoint_set.sizes[real_leader]

        ret = 0
        for leader in leader_size:
            ret += (leader_size[leader] - 1)
        return ret  
```


## Problem Remark 
- We define connected-compoent as the componet of stones share same col/row with at least 1 other stone in the graph
- STEP1, remember all the locations of the stones
- STEP2, create disjoint set that stores all connected-component together 
- STEP3, for each connected component, we greedily pick the size-1 of that component
