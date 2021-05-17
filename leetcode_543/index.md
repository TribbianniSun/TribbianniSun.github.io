# Leetcode_543 Diameter of Binary Tree


Use **DP On Tree** to solve Leetcode_543 Diameter of Binary Tree
<!--more-->


## Problem Description [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)


<p>
Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.
</p>

## Example Test Cases [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)


![test case 2](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)
```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3is the length of the path [4,2,1,3] or [5,2,1,3].
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
    int ret = 0;
    int diameterOfBinaryTree(TreeNode* root) {
        dfs(root);
        return ret - 1;
    }
private:
    int dfs(TreeNode* node){
        if(node == nullptr){
            return 0;
        }
        int l = dfs(node -> left);
        int r = dfs(node -> right);
        ret = max(ret, l + r + 1);
        return max(l, r) + 1;
    }
};
```

