# Leetcode_135 Candy


Use **Greedy** to solve Leetcode 135 - Candy.
<!--more-->




## Problem Solution [Leetcode135 - Candy](https://leetcode.com/problems/candy/)
```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        int n = ratings.size();
        vector<int> ret (n, 1);
        
        for(int i = n - 2; i >= 0; i--){
            if(ratings[i] > ratings[i + 1]) ret[i] = ret[i + 1] + 1;
        }
        
        for(int i = 1; i < n; i++){
            if(ratings[i] > ratings[i - 1]) ret[i] = max(ret[i-1] + 1, ret[i]);
        }
        
        int s = 0;
        for(int i : ret) s += i;
        return s;
    }
};
```


## Solution Proof [Leetcode135 - Candy](https://leetcode.com/problems/candy/)

