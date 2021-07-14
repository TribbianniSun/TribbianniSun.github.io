# Leetcode_133. Clone Graph


Use **dfs** to solve Leetcode 133. Clone Graph.
<!--more-->


## Problem Solution [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    unordered_map<int, Node*> mp;
        
    Node* cloneGraph(Node* node) {
        if(node == nullptr) return nullptr;
        int val = node -> val;
        if(mp.count(val)) return mp[val];
        vector<Node*> fn;
        Node* focusNode = new Node(val, fn);
        mp[val] = focusNode;
        for(auto p : node -> neighbors){
            focusNode -> neighbors.push_back(cloneGraph(p));
        }
        return focusNode;
    }
};
```
