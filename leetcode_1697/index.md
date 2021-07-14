# Leetcode_1697 Checking Existence of Edge Length Limited Paths



Use **union-find, offline-algorithm, graph** to solve Leetcode 1697 Checking Existence of Edge Length Limited Paths.
<!--more-->


## Problem Solution [Leetcode 1697. Checking Existence of Edge Length Limited Paths](https://leetcode.com/problems/checking-existence-of-edge-length-limited-paths/)


<p>
An undirected graph of n nodes is defined by edgeList, where edgeList[i] = [ui, vi, disi] denotes an edge between nodes ui and vi with distance disi. Note that there may be multiple edges between two nodes.

Given an array queries, where queries[j] = [pj, qj, limitj], your task is to determine for each queries[j] whether there is a path between pj and qj such that each edge on the path has a distance strictly less than limitj .

Return a boolean array answer, where answer.length == queries.length and the jth value of answer is true if there is a path for queries[j] is true, and false otherwise.
</p>


## Example Test Cases [Leetcode 1697. Checking Existence of Edge Length Limited Paths](https://leetcode.com/problems/checking-existence-of-edge-length-limited-paths/)
![Example Test Cases I](https://assets.leetcode.com/uploads/2020/12/08/h.png)

```
Input: n = 3, edgeList = [[0,1,2],[1,2,4],[2,0,8],[1,0,16]], queries = [[0,1,2],[0,2,5]]
Output: [false,true]
Explanation: The above figure shows the given graph. Note that there are two overlapping edges between 0 and 1 with distances 2 and 16.
For the first query, between 0 and 1 there is no path where each distance is less than 2, thus we return false for this query.
For the second query, there is a path (0 -> 1 -> 2) of two edges with distances less than 5, thus we return true for this query.
```

## Problem Solution [Leetcode 1697. Checking Existence of Edge Length Limited Paths](https://leetcode.com/problems/checking-existence-of-edge-length-limited-paths/)


```cpp
class Solution {
public:
    static const int N = 1e5 + 10;
    int p[N];

    int find(int x){
        if(p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    
    static bool cmp(vector<int>& a, vector<int>& b){
        return a[2] < b[2];
    }
    
    vector<bool> distanceLimitedPathsExist(int pp, vector<vector<int>>& edgeList, vector<vector<int>>& queries) {
        int n = edgeList.size(), m = queries.size();
        for(int i = 0; i <= pp; i++){
            p[i] = i;
        }
        vector<bool> ret(m, false);
        
        for(int i = 0; i < queries.size(); i++){
            queries[i].push_back(i);
        }
        
        sort(edgeList.begin(), edgeList.end(), cmp);
        sort(queries.begin(), queries.end(), cmp);

        int i = 0, j = 0;
        
        for(;j < m; j++){
            int a = queries[j][0], b = queries[j][1];
            while(i < n and edgeList[i][2] < queries[j][2]){
                int x = edgeList[i][0], y = edgeList[i][1];
                int px = find(x), py = find(y);
                p[px] = py;
                i += 1;
            }
            if(find(a) == find(b)) ret[queries[j][3]] = true;
        }
        
        return ret;
    }
};
```


## Problem Analysis [Leetcode 1697. Checking Existence of Edge Length Limited Paths](https://leetcode.com/problems/checking-existence-of-edge-length-limited-paths/)

- Offline algorithm means that we can sort the queries by its limit
- Once we sort the queries by limit and edges by weight, we can free up edges for each query
- To answer each query, we can do a union-find since the graph is undirected! 
