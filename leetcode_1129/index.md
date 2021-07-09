# Leetcode_1129 Shortest Path with Alternating Colors


Use **graph** to solve Leetcode 1129 Shortest Path with Alternating Colors
<!--more-->


## Problem Solution [1129. Shortest Path with Alternating Colors](https://leetcode.com/problems/shortest-path-with-alternating-colors/)


```cpp
class Solution {
public:
    static const int N = 105;
    int dist_red[N][2];
    int dist_blue[N][2];
    bool st[N][2];
    vector<int> graph_red[N];
    vector<int> graph_blue[N];
    
    inline void bfs(int node, int is_red, int dist[105][2]){
        memset(st, 0, sizeof st);
        dist[node][is_red] = 0;
        queue<int> q;
        
        q.push(node);
        
        int step = 0;
        while(q.size()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                
                int cur = q.front(); q.pop();
                
                if(step % 2 == is_red){
                    for(int next_node : graph_red[cur]){
                        if(dist[next_node][is_red] > step + 1){
                            dist[next_node][is_red] = step + 1;
                            q.push(next_node);
                            if(!st[next_node][is_red]){
                                q.push(next_node);
                                st[next_node][is_red] = true;
                            }
                        }
                    }
                }
                else{
                    for(int next_node : graph_blue[cur]){
                        if(dist[next_node][1 ^ is_red] > step + 1){
                            dist[next_node][1 ^ is_red] = step + 1;
                            q.push(next_node);
                            if(!st[next_node][1 ^ is_red]){
                                q.push(next_node);
                                st[next_node][1 ^ is_red] = true;
                            }
                        }
                    }
                }
            }   
            step += 1;
        }
    }
    
    
    vector<int> shortestAlternatingPaths(int n, vector<vector<int>>& red_edges, vector<vector<int>>& blue_edges) {
        memset(dist_red, 0x3f, sizeof dist_red);
        memset(dist_blue, 0x3f, sizeof dist_blue);
        memset(graph_blue, 0, sizeof graph_blue);
        memset(graph_red, 0, sizeof graph_red);
        
        for(auto& edge : red_edges){
            graph_red[edge[0]].push_back(edge[1]);
        }
        for(auto& edge : blue_edges){
            graph_blue[edge[0]].push_back(edge[1]);
        }
        
        bfs(0, 0, dist_red);
        bfs(0, 1, dist_blue);
        vector<int> ret;
        for(int i = 0; i < n; i++){
            dist_blue[i][0] = min(dist_blue[i][0], dist_blue[i][1]);
            dist_red[i][0] = min(dist_red[i][0], dist_red[i][1]);
            if(dist_blue[i][0] > 0x3f3f3f3f / 2 and dist_red[i][0] > 0x3f3f3f3f / 2) ret.push_back(-1);
            else ret.push_back(min(dist_blue[i][0], dist_red[i][0]));
        }
        
        return ret;
    }
};
```
