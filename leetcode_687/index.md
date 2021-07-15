# Leetcode_687 Longest Univalue Path


Use **dfs** to solve Leetcode 687. Longest Univalue Path
<!--more-->

## Problem Solution [Leetcode 687. Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/)

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

class Solution {
public:
    
    int global_ret = 0;
    
    int dfs(TreeNode* node, int val){
        if(node == nullptr) return 0;

        int l = dfs(node -> left, node -> val);
        int r = dfs(node -> right, node -> val);
        global_ret = max(global_ret, l + r + 1);
        if(node -> val == val){
            return max(l, r) + 1;    
        }
        else{
            return 0;
        }
    }
    
    int longestUnivaluePath(TreeNode* root) {
        if(root == nullptr) return 0;
        dfs(root, -1);
        return global_ret - 1;
    }
};
```
