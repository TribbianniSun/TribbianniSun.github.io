# Leetcode_218. The Skyline Problem


Use **sweep-line** to solve Leetcode_218. The Skyline Problem
<!--more-->

## Problem Solution [Leetcode_218. The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/)


```cpp
typedef pair<int, int> PII;

class Solution {
public:
        
    static bool cmp(PII& a, PII& b){
        // process entering events first
        // if we process leaving events, for a timestamp with both leaving and entering,
        // there is a case when the one entering h2 < h1 and 
        // it will have a duplicate timestamp at that point

        if(a.first != b.first) return a.first < b.first;
        else return a.second > b.second; 
        
    }
    
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        multiset<int> s;
        vector<PII> events;
        vector<vector<int>> ret;
        
        for(vector<int>& b : buildings){
            int start = b[0], end = b[1], height = b[2];
            events.push_back({start, height});
            events.push_back({end, -height});
        }
        
        sort(events.begin(), events.end(), cmp);
        
        for(PII& event : events){
            int timeStamp = event.first, height = event.second;
            
            
            // for entering events, we update the height of the skyline 
            // if height is taller than the tallest in multiset
            if(height > 0){
                int tallest = s.size() ? *s.rbegin() : 0;
                if(height > tallest) ret.push_back({timeStamp, height});
                s.insert(height);
            }
            
            // for leaving events, we update the height of the skyline
            // if the height is lower than the original tallest in multiset
            else{
                int original_tallest = s.size() ? *s.rbegin() : 0;
                s.erase(s.lower_bound(-height));
                int tallest = s.size() ? *s.rbegin() : 0;
                if(tallest < original_tallest) ret.push_back({timeStamp, tallest});
            }
        }
        
        return ret;
        
    }
};
```
