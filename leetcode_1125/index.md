# Leetcode_1125 Smallest Sufficient Team


Use **bitmask, dfs** to solve Leetcode 1125. Smallest Sufficient Team
<!--more-->


## Problem Solution [Leetcode 1125. Smallest Sufficient Team](https://leetcode.com/problems/smallest-sufficient-team/)

```cpp
typedef pair<int, int> PII;
class Solution {
public:
    bool st[66];
    int worker[66], n, m;
    vector<PII> useful_worker;
    
    vector<int> global_ret;
    vector<int> local_ret;
    
    void dfs(int i, int state){
        if(state == (1 << m) - 1){
            if(local_ret.size() < global_ret.size() or global_ret.size() == 0) global_ret = local_ret;
            return;
        }
        
        if(i == n) return;
        dfs(i + 1, state);
        if((useful_worker[i].first | state) > state){
            local_ret.push_back(useful_worker[i].second);
            dfs(i + 1, state | useful_worker[i].first);
            local_ret.pop_back();
        }
    }
    
    static int getCnt(int x){
        int ret = 0;
        for(int i = 0; i < 17; i++){
            if(x & 1 << i) ret += 1;
        }
        return ret;
    }
    
    static bool cmp(PII& a, PII& b){
        return getCnt(a.first) > getCnt(b.first);
    }
    
    vector<int> smallestSufficientTeam(vector<string>& req_skills, vector<vector<string>>& people) {
        unordered_map<string, int> mp;
        
        for(string& s : req_skills){
            if(!mp.count(s)) mp[s] = m++;
        }
        
        for(int i = 0; i < people.size(); i++){
            int c = 0;
            for(string& s : people[i])
                c += (1 << mp[s]);
            worker[n++] = c;
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(i == j) continue;
                if((worker[i] & worker[j]) == worker[i] and !st[j]){
                    st[i] = true;
                    continue;
                }
            }
        }
        
        for(int i = 0; i < n; i++){
            if(!st[i]){
                useful_worker.push_back({worker[i], i});
            }
        }
        
        sort(useful_worker.begin(), useful_worker.end(), cmp);

        n = useful_worker.size();
        
        dfs(0, 0);

        return global_ret;
    }  
};
```
