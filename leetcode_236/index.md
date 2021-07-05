# Leetcode_236 Lowest Common Ancestor of a Binary Tree


Use **dfs** to solve Leetcode 236 - Lowest Common Ancestor of a Binary Tree. 
<!--more-->

## Problem Description [Leetcode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

<p>
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”
</p>


## Example Test Cases [Leetcode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

![236_test_case_1](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```


![236_test_case_2](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```


## Problem Solution [Leetcode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)



```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:

    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        
        TreeNode* l = lowestCommonAncestor(root -> left, p, q);
        TreeNode* r = lowestCommonAncestor(root -> right, p, q);
        if(root == p and (l == q or r == q)) return root;
        if(root == q and (l == p or r == p)) return root;
        if(l == p and r == q) return root;
        if(l == q and r == p) return root;
        if(l != nullptr) return l;
        if(r != nullptr) return r;
        if(root == p) return p;
        if(root == q) return q;
        return nullptr;
    }
};
```


### A quick optimization
No need to worry about the situation where **root** is p or q, and its subtree has the other child node p or q, since from the perspective of **root**'s parent, its opposite subtree will return nullptr in this case. Therefore, if root == p or root == q, we can simply return root to keep good code smell.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        if(root == p or root == q) return root;
        TreeNode* l = lowestCommonAncestor(root -> left, p, q);
        TreeNode* r = lowestCommonAncestor(root -> right, p, q);
        if(l && r) return root;
        return l ? l : r;
    }
};
```
