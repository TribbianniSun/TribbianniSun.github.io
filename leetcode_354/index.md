# Leetcode_354 Russian Doll Envelopes

Use **DP-LIS** to solve Leetcode_354 Russian Doll Envelopes
<!--more-->


## Problem Description [Leetcode 354](https://leetcode.com/problems/russian-doll-envelopes/)

<p>
You are given a 2D array of integers envelopes where envelopes[i] = [wi, hi] represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope are greater than the other envelope's width and height.

Return the maximum number of envelopes you can Russian doll (i.e., put one inside the other).

Note: You cannot rotate an envelope.
</p>

## Example Test Cases [Leetcode 354](https://leetcode.com/problems/russian-doll-envelopes/)

```
Input: envelopes = [[5,4],[6,4],[6,7],[2,3]]
Output: 3
Explanation: The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```

## Problem Solution [Leetcode 354](https://leetcode.com/problems/russian-doll-envelopes/)


```cpp
class Solution {
public:
    static bool comp(vector<int>& a, vector<int>& b){
        if(a[0] != b[0]) return a[0] < b[0];
        else return a[1] > b[1];
    }
    int maxEnvelopes(vector<vector<int>>& e) {
        sort(e.begin(), e.end(), comp);
        set<int> s;
        for(auto t : e){
            int n = t[1];
            auto it = s.lower_bound(n);
            if(it != s.end()) s.erase(it);
            s.insert(n);
        }
        return s.size();
        
    }
};
```
