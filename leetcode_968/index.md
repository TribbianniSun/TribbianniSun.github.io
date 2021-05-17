# Leetcode_968 Binary Tree Cameras



Use **DP-On-Tree** to solve Leetcode_968 Binary Tree Cameras
<!--more-->


## Problem Description [Leetcode 968](https://leetcode.com/problems/binary-tree-cameras/)

<p>
Given a binary tree, we install cameras on the nodes of the tree. 

Each camera at a node can monitor its parent, itself, and its immediate children.

Calculate the minimum number of cameras needed to monitor all nodes of the tree.
</p>


## Example Test Cases [Leetcode 968](https://leetcode.com/problems/binary-tree-cameras/)

![Example1](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_01.png)
```
Input: [0,0,null,0,0]
Output: 1
Explanation: One camera is enough to monitor all nodes if placed as shown.
```

![Example2](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_02.png)
```
Input: [0,0,null,0,null,0,null,null,0]
Output: 2
Explanation: At least two cameras are needed to monitor all nodes of the tree. The above image shows one of the valid configurations of camera placement.
```

## Problem Solution [Leetcode 968](https://leetcode.com/problems/binary-tree-cameras/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minCameraCover(self, root: TreeNode) -> int:
        if root == None:
            return 0
        mp = {}
        mp[(None, 0)] = 0 # cover by its children
        mp[(None, 1)] = 2e9 # cover by itself, impossible for None
        mp[(None, 2)] = 0 # cover by its parent
        def dfs(node):
            nonlocal mp
            if node == None:
                return 
            if node.left == None and node.right == None:
                mp[(node, 0)] = 2e9 # cover by its childre, impossible for leaf node
                mp[(node, 1)] = 1
                mp[(node, 2)] = 0
                return
            dfs(node.left)
            dfs(node.right)
            mp[(node, 1)] = min(mp[(node.left, 1)], mp[(node.left, 2)], mp[(node.left, 0)]) + min(mp[(node.right, 1)], mp[(node.right, 2)], mp[(node.right, 0)]) + 1
            mp[(node, 0)] = min(mp[(node.left, 1)] + mp[(node.right, 1)], mp[(node.left, 0)] + mp[(node.right, 1)],  mp[(node.left, 1)] + mp[(node.right, 0)])
            mp[(node, 2)] = min(mp[(node.left, 1)], mp[(node.left, 0)]) + min(mp[(node.right, 1)], mp[(node.right, 0)])
            return
        
        dfs(root)
        return min(mp[(root,0)], mp[(root,1)])     
```


## Problem Remark [Leetcode 968](https://leetcode.com/problems/binary-tree-cameras/)
- dp[i][0] -> for the set of all the nodes(within subtree whose root is i), we cover them by its children
- dp[i][1] -> for the set of all the nodes(within subtree whose root is i), we cover them by itself
- dp[i][2] -> for the set of all the nodes(within subtree whose root is i), we cover them by its parent
- DP On Tree + DP-State-Machine 

