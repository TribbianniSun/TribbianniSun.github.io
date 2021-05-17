# Leetcode_124 Binary Tree Maximum Path Sum



Use **DP On Tree** to solve Leetcode_124 Binary Tree Maximum Path Sum
<!--more-->


## Problem Description [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

<p>
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any path.
</p>


## Example Test Cases [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

![test case 2](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```



## Problem Solution [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

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
    int ret = -2e9;
    int maxPathSum(TreeNode* root) {
        dfs(root);
        return ret;
    }
private:
    int dfs(TreeNode* node){
        if(node == nullptr){
            return 0;
        }
        int l = dfs(node -> left);
        int r = dfs(node -> right);
        int c = max(l, 0) + max(r, 0) + node -> val;
        ret = max(ret, c);
        // node->val
        // node->val + l
        // node->val + r
        // 0
        return max(max(0, node->val), max(node->val + l, node->val + r));
    }
};
```


## Problem Remark [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
- For the return value, it could be the max among these four: node->val, node -> val + l, node -> val + r, 0

