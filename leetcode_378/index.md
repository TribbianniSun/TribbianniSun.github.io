# Leetcode_378 Kth Smallest Element in a Sorted Matrix



Use **data-structure, binary-search** to solve Leetcode 378 Kth Smallest Element in a Sorted Matrix.
<!--more-->

## Problem Solution [Leetcode 378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)


### Binary-Search Solution -> O(n * log(max - min))


```cpp
class Solution {
public:
    int check(int num, vector<vector<int>>& matrix, int k){
        int n = matrix.size();
        int ret = 0, j = n - 1;
        for(int i = 0; i < n; i++){
            while(j != -1 and matrix[i][j] > num) j -= 1;
            ret += (j + 1);
        }
        return ret < k;
    }
    
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        int l = matrix[0][0], r = matrix[n-1][n-1];    
        while(l < r){
            int mid = (l + r) / 2;
            if(check(mid, matrix, k)) l = mid + 1;
            else r = mid;
        }
        return r;
    }
};
```

#### Would the answer eventuall be in the array?
- Yes! 
- Since we are always conducting binary-search, and the search result would eventually converge to some number equal to the kth smallest number, therefore, the answer will be inside the array, and binary search works here.

### Heap Solution -> O(k * logn)

```cpp
typedef pair<int, int> PII;

class Solution {
public:
    
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        
        int n = matrix.size();
        priority_queue<PII, vector<PII>, greater<PII>> pq;
        for(int i = 0; i < n; i++){
            int val = matrix[i][0];
            int t = i * n + 0;
            pq.push({val, t});
        }
        
        for(int i = 0; i < k - 1; i++){
            auto t = pq.top(); pq.pop();
            int idx = t.second;
            int val = t.first;
            int ni = idx / n, nj = idx % n;
            nj += 1;
            if(nj == n) continue;
            pq.push({matrix[ni][nj], ni * n + nj});
        }
        
        return pq.top().first;
    }
};
```
