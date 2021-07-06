# Leecode_1338 Reduce Array Size to The Half




Use **data-structure** to solve Leetcode_1338 Reduce Array Size to The Half
<!--more-->


## Problem Solution [Leetcode 1338. Reduce Array Size to The Half](https://leetcode.com/problems/reduce-array-size-to-the-half/)

```cpp
typedef pair<int, int> PII;
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        unordered_map<int, int> mp;
        for(int num : arr){
            mp[num] += 1;
        }
        
        priority_queue<PII> pq;
        for(auto&& [num, freq] : mp){
            pq.push({freq, num});
        }
        int ret = 0, counter = 0, target = (arr.size() + 1) / 2;
        
        while(counter < target){
            auto t = pq.top(); pq.pop();
            ret += 1;
            counter += t.first;
        }
        
        return ret;
    }
};
```



## Problem Solution [Leetcode 1338. Reduce Array Size to The Half](https://leetcode.com/problems/reduce-array-size-to-the-half/)

- Basically, we can store the frequency of frequency to reduce the runtime from O(logn) -> O(n)

```cpp
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        unordered_map<int, int> mp;
        for(int num : arr){
            mp[num] += 1;
        }
        
        int freq[100005];
        memset(freq, 0, sizeof freq);
        
        int max_f = 0;
        for(auto&& [num, f] : mp){
            freq[f] += 1;
            max_f = max(max_f, f);
        }
        
        int counter = 0, ret = 0, target = (arr.size() + 1) / 2;
        
        for(int i = max_f; i >= 0 and counter < target; i--){
            for(int j = 0; j < freq[i] and counter < target; j++){
                counter += i;
                ret += 1;
            }
        }
        
        return ret;
    }
};
```


