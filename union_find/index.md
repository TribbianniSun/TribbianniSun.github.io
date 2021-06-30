# union-find Review


This article reviews union-find(Disjoint Set).
<!--more-->

# union-find | Disjoint Set

### Semantics
- This data structure stores the collection of disjoint(non-overlapping) sets(groups). 
- *find(p):* find the leader of group that contains p
- *union(p, q):* merge two groups



### Implementation
```python
class UnionFind(object):
    def __init__(self):
        self.num_sets = 0
        self.parents = {}
        self.sizes = {}

    def contains(self, p):
        return p in self.parents


    def insert(self, p):
        if self.contains(p):
            return
        else:
            self.parents[p] = p
            self.sizes[p] = 1
            self.num_sets += 1

    def find(self, p):
        if p != self.parents[p]:
            self.parents[p] = self.find(self.parents[p])
            p = self.parents[p]
        return self.parents[p]


    def union(self, p, q):
        root_p, root_q = self.find(p), self.find(q)
        if root_p == root_q:
            return
        else:

            if self.sizes[root_p] > self.sizes[root_q]:
                small_root = root_q
                large_root = root_p
            else:
                small_root = root_p
                large_root = root_q
            
            self.parents[small_root] = large_root
            self.sizes[large_root] += self.sizes[small_root]
            self.num_sets -= 1
```


### Efficienty Analysis
- **O(n)** in memory, **O(1)** for union and look up in amortized analysis 


### Remarks
- Check whether two elements belong to the same group.
- To find connected components in graph (usually undirected)
- Speed up implementation of kruskal's algorithm 

