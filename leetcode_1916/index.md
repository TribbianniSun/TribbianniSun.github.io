# Leetcode_1916. Count Ways to Build Rooms in an Ant Colony



Use **math, dfs** to solve Leetcode 1916. Count Ways to Build Rooms in an Ant Colony
<!--more-->



## Problem Description [Leetcode 1916. Count Ways to Build Rooms in an Ant Colony](https://leetcode.com/problems/count-ways-to-build-rooms-in-an-ant-colony/)

<p>
You are an ant tasked with adding n new rooms numbered 0 to n-1 to your colony. You are given the expansion plan as a 0-indexed integer array of length n, prevRoom, where prevRoom[i] indicates that you must build room prevRoom[i] before building room i, and these two rooms must be connected directly. Room 0 is already built, so prevRoom[0] = -1. The expansion plan is given such that once all the rooms are built, every room will be reachable from room 0.

You can only build one room at a time, and you can travel freely between rooms you have already built only if they are connected. You can choose to build any room as long as its previous room is already built.

Return the number of different orders you can build all the rooms in. Since the answer may be large, return it modulo 1e9 + 7.
</p>




## Example Test Cases [Leetcode 1916. Count Ways to Build Rooms in an Ant Colony](https://leetcode.com/problems/count-ways-to-build-rooms-in-an-ant-colony/)

```
Input: prevRoom = [-1,0,0,1,2]
Output: 6
Explanation:
The 6 ways are:
0 → 1 → 3 → 2 → 4
0 → 2 → 4 → 1 → 3
0 → 1 → 2 → 3 → 4
0 → 1 → 2 → 4 → 3
0 → 2 → 1 → 3 → 4
0 → 2 → 1 → 4 → 3
```



## Problem Solution [Leetcode 1916. Count Ways to Build Rooms in an Ant Colony](https://leetcode.com/problems/count-ways-to-build-rooms-in-an-ant-colony/)

```python
class Solution:
    
    def waysToBuildRooms(self, prevRoom: List[int]) -> int:
        mod = int(1e9 + 7)
        d = {}
        n = len(prevRoom)
        cnt = [0 for _ in range(n)]
        ways = [0 for _ in range(n)]
        
        
        # calculates choose a from b
        
        def comb(n, k):
            if((n, k) in d):
                return d[(n, k)]
            if(k > n):
                return 0
            if (k * 2 > n):
                k = n-k
            if (k == 0):
                return 1
            ret = n
            for i in range(2, k + 1, 1):
                ret *= (n - i + 1)
                ret = ret // i
            d[(n, k)] = ret % mod
            return ret % mod

        
        
        graph = [[] for _ in range(n)]
        for i in range(n):
            if prevRoom[i] == -1:
                continue
            graph[prevRoom[i]].append(i)
        

        def dfs(node):
            c_cnt = 1
            for i in graph[node]:
                dfs(i)
                c_cnt += cnt[i]
            cnt[node] = c_cnt
            
            c_way = 1
            for i in graph[node]:
                c_way = (c_way * comb(c_cnt - 1, cnt[i])) % mod 
                c_way = (c_way * ways[i]) % mod
                c_cnt -= cnt[i]
                
            ways[node] = c_way
            
            return ways[node] % mod
        
        dfs(0)
        return ways[0]
```



## Problem Analysis [Leetcode 1916. Count Ways to Build Rooms in an Ant Colony](https://leetcode.com/problems/count-ways-to-build-rooms-in-an-ant-colony/)
- ways[i] means the number of ways to build rooms in subtree with node i
- cnt[i] means how many nodes 
- if we want to update ways[node], we need to enumerate all its children c1, c2 ... cn
    - First, we choose cnt[ci] from sum(cnt[ci])
    - Then we have ways[ci] to consider
    - Just apply multiply rule, multiply all the numbers, and we are good to go
