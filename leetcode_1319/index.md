# Leetcode_1319 Number of Operations to Make Network Connected




Use **union-find 维护集合数的并查集** to solve Leetcode 1319 - Number of Operations to Make Network Connected
<!--more-->




## Problem Description [Leetcode 1319](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

<p>

There are n computers numbered from 0 to n-1 connected by ethernet cables connections forming a network where connections[i] = [a, b] represents a connection between computers a and b. Any computer can reach any other computer directly or indirectly through the network.

Given an initial computer network connections. You can extract certain cables between two directly connected computers, and place them between any pair of disconnected computers to make them directly connected. Return the minimum number of times you need to do this in order to make all the computers connected. If it's not possible, return -1. 

</p>






## Example Test Cases [Leetcode 1319](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

```
Input: n = 6, connections = [[0,1],[0,2],[0,3],[1,2],[1,3]]
Output: 2
```

## Problem Solution [Leetcode 1319](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

```cpp
class Solution {
public:
    int p[100005];
    int find(int a){
        if(p[a] != a) return p[a] = find(p[a]);
        return p[a];
    }
    int makeConnected(int n, vector<vector<int>>& c) {
        for(int i = 0; i < n; i++){
            p[i] = i;
        }
        int s = c.size();
        for(int i = 0; i < s; i++){
            int a = c[i][0], b = c[i][1];
            int pa = find(a), pb = find(b);
            p[pa] = pb;
        }
        int group = 0;
        for(int i = 0; i < n; i++){
            if(p[i] == i) group += 1;
        }

        // group - 1 wires needed to be changed
        if(s < n - 1) return -1;
        else return group - 1;
    }
};
```


