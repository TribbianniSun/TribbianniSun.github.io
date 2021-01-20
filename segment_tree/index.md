# Segment Tree review


This article reviews Segment Tree.
<!--more-->

# Segment Tree

### Semantics
- This balanced tree data structure stores the aggregation of certain property within certain range. 
- *build(start, end, vals):* construct the segment tree
- *update(index, value):* update the A[index] to value
- *rangeQuery(start, end)* query the aggregation of certain range [start, end]


### Implementation
```python
class SegmentTreeNode:
    def __init__(self, start, end, val, left=None, right=None):
        self.start = start
        self.end = end
        self.mid = start + (end - start) // 2
        self.val = val
        self.left = left
        self.right = right


class SegmentTree:
    def __init__(self, nums):
        self.nums = nums
        if self.nums:
            self.root = self.build(0, len(nums) - 1, nums)
    

    def build(self, start, end, nums):
        if start == end:
            return SegmentTreeNode(start, end, nums[start])
        
        mid = (end - start) // 2 + start
        leftNode = self.build(start, mid, nums)
        rightNode = self.build(mid + 1, end, nums)
        return SegmentTreeNode(start, end, leftNode.val + rightNode.val, leftNode, rightNode)



    def update(self, index, value):
        self.updateHelper(self.root, index, value)

    def updateHelper(self, node, index, value):
        if node.start == index and node.end == index:
            node.val = value
            return
        if index <= node.mid:
            self.updateHelper(node.left, index, value)
        else:
            self.updateHelper(node.right, index, value)
        
        node.val = node.left.val + node.right.val


    def queryRange(self, start, end):
        return self.queryRangeHelper(self.root, start, end)

    def queryRangeHelper(self, node, start, end):
        if node.start == start and node.end == end:
            return node.val
        elif end <= node.mid:
            return self.queryRangeHelper(node.left, start, end)
        elif start > node.mid:
            return self.queryRangeHelper(node.right, start, end)
        else:
            return self.queryRangeHelper(node.left, start, node.mid) + self.queryRangeHelper(node.right, node.mid + 1, end)



```


### Efficienty Analysis
- buil -> **O(n)** 
- update -> **O(log n)** 
- rangeQuery -> **~ O(log n)** 

### Remarks
- query range with mutable arrays


