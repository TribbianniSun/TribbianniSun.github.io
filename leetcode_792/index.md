# Leetcode_792


Use **Data Structure** to solve Leetcode 792 - Number of Matching Subsequences.
<!--more-->


## Problem Solution [Leetcode 792 - Number of Matching Subsequences
](https://leetcode.com/problems/number-of-matching-subsequences/)

```cpp

// a -> [a, acd, ace]
// b -> [bb]

// b -> [bb]
// c -> [cd, ce]
// O(|S| + n * |s|)

typedef pair<int, int> PII;

class Solution {
public:
    
    int numMatchingSubseq(string s, vector<string>& words) {
        unordered_map<char, vector<PII>> mp;
        int ret = 0;
        for(int i = 0; i < words.size(); i++){
            char c = words[i][0];
            if(mp.count(c)){
                mp[c].push_back({i, 0});
            }
            else{
                vector<PII> cur;
                cur.push_back({i, 0});
                mp[c] = cur;
            }
        }
        for(int i = 0; i < s.size(); i++){
            char c = s[i];
            if(mp.count(c)){
                bool flag = false;
                vector<PII> remain;
                for(auto t : mp[c]){
                    int idxInWords = t.first, idxInWord = t.second;
                    idxInWord+=1;
                    if(idxInWord == words[idxInWords].size()){
                        ret += 1;
                        continue;
                    }
                    else{
                        char nc = words[idxInWords][idxInWord];
                        if(nc == c){
                            flag = true;
                            remain.push_back({idxInWords, idxInWord});
                            continue;
                        }
                        if(mp.count(nc)){
                            mp[nc].push_back({idxInWords, idxInWord});
                        }
                        else{
                            vector<PII> cur;
                            cur.push_back({idxInWords, idxInWord});
                            mp[nc] = cur;
                        }
                    }
                }
                mp[c].clear();
                if(flag){
                    mp[c] = remain;
                }
            }
        }
        return ret;
    }
};
```
