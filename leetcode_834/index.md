# Leetcode_834 Sum of Distance in Tree



New **dp** to solve Leetcode 834 - Sum of Distance in Tree.
<!--more-->


## Problem Description [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/)

<p>
An undirected, connected tree with n nodes labelled 0...n-1 and n-1 edges are given.

The ith edge connects nodes edges[i][0] and edges[i][1] together.

Return a list ans, where ans[i] is the sum of the distances between node i and all other nodes.
</p>




## Example Test Cases [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/)

```
Input: n = 6, edges = [[0,1],[0,2],[2,3],[2,4],[2,5]]
Output: [8,12,6,10,10,10]
Explanation: 
Here is a diagram of the given tree:
  0
 / \
1   2
   /|\
  3 4 5
We can see that dist(0,1) + dist(0,2) + dist(0,3) + dist(0,4) + dist(0,5)
equals 1 + 1 + 2 + 2 + 2 = 8.  Hence, answer[0] = 8, and so on.
```




## Problem Solution [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/)

```cpp
class Solution {
public:
    int cnt[10000 + 5], sum[10000 + 5], ret[10000 + 5];
    
    vector<int> graph[10000 + 5];
    int root = -1;
    
    
    int find_count(int node, int parent){
        int ret = 1;
        for(int i : graph[node]){
            if(i != parent)
                ret += find_count(i, node);
        }
        return cnt[node] = ret;
    }
    
    int find_sum(int node, int parent){
        int ret = -1 + cnt[node];
        for(int i : graph[node]){
            if(i != parent)
                ret += find_sum(i, node);
        }
        return sum[node] = ret;
    }
    
    void find_ret(int node, int parent){
        if(parent == -1){
            int cret = -1 + cnt[root];
            for(int i : graph[node]){
                cret += sum[i];
            }
            ret[node] = cret;
        }
        else{
            ret[node] = ret[parent] + cnt[root] - cnt[node] * 2;
        }
        
        for(int i : graph[node]){
            if(i != parent)
                find_ret(i, node);
        }
        return;
        
    }
    vector<int> sumOfDistancesInTree(int n, vector<vector<int>>& edges) {
        unordered_set<int> non_root;
        for(auto e : edges){
            int a = e[0], b = e[1];
            graph[a].push_back(b);  
            graph[b].push_back(a); 
        }
    
        root = 0;
        find_count(root, -1);
        find_sum(root, -1);
        find_ret(0, -1);
        vector<int> global_ret;
        for(int i = 0; i < n; i++){
            global_ret.push_back(ret[i]);
        }
        return global_ret;
    }
};


// cnt[2] = 4
// cnt[node] -> 以node为根的，子树，节点数量
// sum[node] -> -1 + cnt[node] + sum[node.i], sum[node.j], sum[node.k ...] -> 以node为根的，只考虑子树的，和

// cnt[0] = 6
// sum[0] = -1 + cnt[0] + sum[1] + sum[2] = -1 + 6 + 0 + 3 = 8
// sum[1] = 0
// sum[2] = 3

// sum[0] = 8

// 
// ret[node] = sum[node] + ret[parent] + n - cnt[node] - sum[node] - cnt[node] = ret[parent] + n - cnt[node] * 2 = 8 + 6 - 4 * 2 = 6
// ret[1] = 8 + 6 - 2 = 12

```



## Problem Analysis [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/)
- cnt[node] -> 以node为根的，子树，节点数量
- sum[node] -> 以node为根的，只考虑子树的，路径和 -> sum[node] = -1 + cnt[node] + sum[node.i], sum[node.j], sum[node.k ...] where node.t is node's child
- ret[node] = sum[node] + ret[parent] + n - cnt[node] - sum[node] - cnt[node] = ret[parent] + n - cnt[node] * 2
- dfs 3 times

