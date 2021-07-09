# Leetcode_1514 Path with Maximum Probability



Use **graph, dijkstra** to solve Leetcode 1514 Path with Maximum Probability.
<!--more-->

## Problem Solution [Leetcode 1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/)

```cpp
typedef pair<double, int> PDI;

class Solution {
public:
    
    static const int N = 1e4 + 10;
    double INF = -1e9;
    vector<PDI> graph[N];
    double dist[N];
    bool st[N];
    
    inline void build(vector<vector<int>>& edges, vector<double>& succProb){
        for(int i = 0; i < edges.size(); i++){
            int a = edges[i][0], b = edges[i][1];
            double w = succProb[i];
            graph[a].push_back({w, b});
            graph[b].push_back({w, a});
        }
    }
    
    inline void dijkstra(int start, int n){
        memset(st, 0, sizeof st);
        for(int i = 0; i <= n; i++) dist[i] = INF;
        priority_queue<PDI> pq;
        dist[start] = 1;
        pq.push({1.0, start});
        
        while(pq.size()){
            auto p = pq.top(); pq.pop();
            double a = p.first;
            int b = p.second;
            if(st[b]) continue;
            st[b] = true;
            for(auto np : graph[b]){
                double weight = np.first;
                int vertex = np.second;
                if(dist[vertex] < a * weight){
                    dist[vertex] = a * weight;
                    pq.push({dist[vertex], vertex});
                }
            }
        }
    }
    
    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end) {
        build(edges, succProb);
        dijkstra(start, n);
        return dist[end] == INF ? 0 : dist[end];
    }
};
```
