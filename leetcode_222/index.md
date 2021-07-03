# Leetcode_222 Count Complete Tree Nodes



New **binary-search** to solve Leetcode 222 - Count Complete Tree Nodes
<!--more-->


## Problem Description [Leetcode 222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)

<p>
Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.

</p>


## Example Test Cases [Leetcode 222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)


![test case leetcode 222](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)
```
Input: root = [1,2,3,4,5,6]
Output: 6
```




## Problem Solution [Leetcode 222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)
 
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
    
    bool check(TreeNode* root, int number){
        if(number == 0) return true;
        int max_bit = ceil(log2(number));
        if(number & 1 << max_bit){
            
        }
        else{
            max_bit -= 1;
        }
        for(int i = max_bit - 1; i >= 0; i--){
            if(number & (1 << i)){
                root = root -> right;
            }
            else{
                root = root -> left;
            }
            if(root == nullptr) return false;
        }
        
        return true;
    }
    
    int countNodes(TreeNode* root) {
        if(root == nullptr) return 0;
        int l = 0, r = 5e4 + 10;
        while(l < r){
            int mid = (l + r + 1) / 2;
            if(check(root, mid)) l = mid;
            else r = mid - 1;
        }
        
        return l;
    }
};
```
