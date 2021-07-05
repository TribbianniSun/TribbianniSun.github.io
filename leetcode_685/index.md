# Leetcode_685 Redundant Connection II



Use **union-find** to solve Leetcode 685 Redundant Connection II.
<!--more-->


## Problem Description [685 Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/)

<p>
In this problem, a rooted tree is a directed graph such that, there is exactly one node (the root) for which all other nodes are descendants of this node, plus every node has exactly one parent, except for the root node which has no parents.

The given input is a directed graph that started as a rooted tree with n nodes (with distinct values from 1 to n), with one additional directed edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed.

The resulting graph is given as a 2D-array of edges. Each element of edges is a pair [ui, vi] that represents a directed edge connecting nodes ui and vi, where ui is a parent of child vi.

Return an edge that can be removed so that the resulting graph is a rooted tree of n nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array.
</p>


## Example Test Cases [685 Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/)

```
Input: edges = [[1,2],[2,3],[3,4],[4,1],[1,5]]
Output: [4,1]
```


## Problem Solution (Brute Force) [685 Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/)

```cpp
class Solution {
public:
    
    vector<int> f[1005];
    bool seen[1005];
    int indegree[1005];
    
    bool check(int idx, vector<vector<int>>& edges){
        
        memset(f, 0, sizeof f);
        memset(seen, 0, sizeof seen);
        memset(indegree, 0, sizeof indegree);
        
        int n = edges.size();
        for(int i = 0; i < n; i++){
            if(i == idx)
                continue;
            int a = edges[i][0], b = edges[i][1];
            f[a].push_back(b);    
            indegree[b] += 1;
        }
        
        int root = -1;
        for(int i = 1; i <= n; i++){
            if(indegree[i] == 0){
                if(root == -1)
                    root = i;
                else
                    return false;
            }
        }
        
        queue<int> q;
        q.push(root);
        seen[root] = true;
        int cnt = 1;
        while(q.size()){
            int c = q.front();
            q.pop();
            for(int i : f[c]){
                if(seen[i]) continue;
                q.push(i);
                seen[i] = true;
                cnt += 1;
            }
        }
        
        return cnt == n;   
    }


    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        for(int i = n - 1; i >= 0; i --){
            if(check(i, edges)){
                return edges[i];
            }
        }
        vector<int> ret;
        return ret;
    }
};
```



## Problem Solution (Smart Union-Find) [685 Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/)

```cpp
class Solution {
public:
    int p[1005];
    int find(int x){
        if(p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    
    int in_node[1005];
    
    vector<int> detect_cycle(vector<vector<int>>& edges){
        vector<int> ret;
        int n = edges.size();
        for(int i = 1; i <= n; i++) p[i] = i;
        for(int i = 0; i < n; i++){
            int a = edges[i][0], b = edges[i][1];
            int pa = find(a), pb = find(b);
            if(pa == pb){
                return edges[i];
            }
            else{
                p[pa] = pb;
            }
        }
        
        return ret;
    }
    
    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        vector<int> candA, candB;
        
        for(int i = 0; i < n; i++){
            int a = edges[i][0], b = edges[i][1];
            if(in_node[b] != 0){
                candA = {in_node[b], b};
                candB = {a, b};
                edges[i][0] = 0;
            }
            else{
                in_node[b] = a;
            }
        }                
        
        vector<int> ret = detect_cycle(edges);
        
        // case 1 : just perform union-find to find cycle
        if(candA.size() == 0) return ret;
        
        // case 2-1
        if(ret.size() == 0) return candB;
        // case 2-2
        return candA;
    }
};
```



## Problem Analysis


### Brute-Force O(n^2)
- Check each edge from back, try to remove it
- If the graph is connected, then that is the answer
- The time complexity is O(n^2)


### Smart Union-Find 
1. If every node only has one single parent => then the redundant edge must form a cycle in the graph, we do a union-find to find that answer

2. If there is a node where there are two edges coming into it, let it be candA and candB, and we let canB appears after candA
    1. First we assume that candB is the answer, we nullify the edge candB
    2. We conduct a union-find to verify the assumption in step 2.1; 
        - if remove candB can make no cycle in graph, candB is the answer
        - otherwise candA is the answer, and we blame candB incorrectly.
3. Some optimization we can make is that, we can clean the code a little bit to combine the union-find together
