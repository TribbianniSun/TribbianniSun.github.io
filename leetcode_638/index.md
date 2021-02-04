# Leetcode_638 Shopping Offers


Use **Dynamic Programming** to solve Leetcode 638 - Shopping Offers. 
<!--more-->


## Problem Description [Leetcode 638](https://leetcode.com/problems/shopping-offers/)

<p>

In LeetCode Store, there are some kinds of items to sell. Each item has a price.

However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

You are given the each item's price, a set of special offers, and the number we need to buy for each item. The job is to output the lowest price you have to pay for exactly certain items as given, where you could make optimal use of the special offers.

Each special offer is represented in the form of an array, the last number represents the price you need to pay for this special offer, other numbers represents how many specific items you could get if you buy this offer.

You could use any of special offers as many times as you want.


</p>



## Examples Test Cases [Leetcode 638](https://leetcode.com/problems/shopping-offers/)


<br>
Example1:
<br>

```
Input: [2,5], [[3,0,5],[1,2,10]], [3,2]
Output: 14
Explanation: 
There are two kinds of items, A and B. Their prices are $2 and $5 respectively. 
In special offer 1, you can pay $5 for 3A and 0B
In special offer 2, you can pay $10 for 1A and 2B. 
You need to buy 3A and 2B, so you may pay $10 for 1A and 2B (special offer #2), and $4 for 2A.
```


<br>
Example2:
<br>


```
Input: [2,3,4], [[1,1,0,4],[2,2,1,9]], [1,2,1]
Output: 11
Explanation: 
The price of A is $2, and $3 for B, $4 for C. 
You may pay $4 for 1A and 1B, and $9 for 2A ,2B and 1C. 
You need to buy 1A ,2B and 1C, so you may pay $4 for 1A and 1B (special offer #1), and $3 for 1B, $4 for 1C. 
You cannot add more items, though only $9 for 2A ,2B and 1C.
```


## Problem Solution [Leetcode 638](https://leetcode.com/problems/shopping-offers/)

```cpp

class Solution {
public:
    unordered_map<string, int> cache;
    vector<int> _p;
    vector<vector<int>> _s;

    string vector2str(vector<int>& num){
        vector<char> v;
        for(int i = 0; i < num.size(); ++i){
            v.push_back('a' + num[i]);
        }

        string s(v.begin(), v.end());
        return s;
    }
    
    int helper(vector<int>& state){
        
        string s = vector2str(state);
        if(cache.find(s) != cache.end()){
            return cache[s];
        }

        int ret = 0;
        for(int i = 0; i < state.size(); ++i){
            ret += (state[i] * _p[i]);
        }

        for(int i = 0; i < _s.size(); ++i){
            vector<int> ns = state;
            int j;
            for(j = 0; j < _s[i].size() - 1; j++){
                ns[j] -= _s[i][j];
                if(ns[j] < 0){
                    break;
                }
            }
            
            if(j == _s[i].size() - 1){
                ret = min(ret, _s[i][j] + helper(ns));
            }
        }

        return cache[vector2str(state)] = ret;

    }

    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        _p  = price;
        _s = special;
        vector<int> startState(needs.size(), 0);
        cache[vector2str(startState)] = 0;
        return helper(needs);
    }
};

```


## Problem Remark 
- Recursion + Memorization
- Top Down, and We can simply try to buy all the items by the original price as the starting ret to compare later. 

