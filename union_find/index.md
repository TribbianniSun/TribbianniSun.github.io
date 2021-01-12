# union_find review


This article reviews union find (AKA disjoint set).
<!--more-->

# Union Find | Disjoint Set

### Semantics
- This data structure stores the collection of disjoint(non-overlapping) sets(groups). 
- *find(p):* find the leader of group that contains p
- *union(p, q):* merge two groups



### Implementation
```python
class UnionFind():
    def __init__(self):
        self.parents = {}
        self.sizes = {}
        self.n_sets = 0

    def contains(self, i):
        return i in self.parents

    def insert(self, i):
        if self.contains(i):
            return
        
        else:
            self.parents[i] = i
            self.sizes[i] = 1
            self.n_sets += 1

    def find(self, i):

        
        while i != self.parents[i]:
            self.parents[i] = self.find(self.parents[i])
            i = self.parents[i]
        return self.parents[i]

    def union(self, p, q):
        root_p, root_q = self.find(p), self.find(q)
        if root_p == root_q:
            return 
        else:
            # we merge the small group into the large group
            small, large = sorted([root_p, root_q], key=lambda x: self.sizes[x])
            self.parents[small] = large

            # fix the size, and decrease the n_sets since we form two groups into a larger group
            self.sizes[big] += self.sizes[small]    
            self.n_sets -= 1
```


### Efficienty Analysis
- **O(n)** in memory, **O(1)** for union and look up in amortized analysis 


### Remarks
- Check whether two elements belong to the same group.
- To find connected components in graph (usually undirected)
- Speed up implementation of kruskal's algorithm 

