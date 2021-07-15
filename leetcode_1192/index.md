# Leetcode_1192 Critical Connections in a Network



Use **graph, Tarjan** to solve Leetcode 1192 Critical Connections in a Network
<!--more-->


## Problem Description [leetcode 1192](https://leetcode.com/problems/critical-connections-in-a-network/)
<p>

There are n servers numbered from 0 to n - 1 connected by undirected server-to-server connections forming a network where connections[i] = [ai, bi] represents a connection between servers ai and bi. Any server can reach other servers directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.
</p>


## Example Test Cases [leetcode 1192](https://leetcode.com/problems/critical-connections-in-a-network/)


![Test Case leetcode 1192](https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png)
```
Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
```


## Problem Solution [leetcode 1192](https://leetcode.com/problems/critical-connections-in-a-network/)


```cpp
class Solution {
public:
    static const int N = 1e5 + 10;
    
    vector<int> graph[N];
    stack<int> myStack;
    
    int dfn[N], low[N], timestamp;
    int id[N], dcc_cnt;
    int indegree[N];
    vector<vector<int>> bridges;
    
    void tarjan(int u, int from){
        
        dfn[u] = low[u] = timestamp++;
        myStack.push(u);
        
        for(int j : graph[u]){
            if(!dfn[j]){
                tarjan(j, u);
                low[u] = min(low[u], low[j]);
                
                if (dfn[u] < low[j])
                    bridges.push_back({u,j});
            }
            else if (j != from)
                low[u] = min(low[u], dfn[j]);
        }
        
        
        if(low[u] == dfn[u]){
            dcc_cnt += 1;
            int y;
            do{
                y = myStack.top(); myStack.pop();
                id[y] = dcc_cnt;
            }while (y != u); 
        }
    }
    
    
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        for(vector<int>& c : connections){
            int a = c[0], b = c[1];
            graph[a].push_back(b), graph[b].push_back(a);
        }
        
        tarjan(0, -1);
        return bridges;
        
    }
};
```




