# Leetcode_1049 Last Stone Weight II



Use **DP-Knapsack-Problem** to solve Leetcode 1049 - Last Stone Weight II. 
<!--more-->


## Problem Description [Leetcode 1049](https://leetcode.com/problems/last-stone-weight-ii/)

<p>

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Suppose the stones have weights x and y with x <= y. The result of this smash is:

- If x == y, both stones are destroyed, and
- If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.

At the end of the game, there is at most one stone left.

Return the smallest possible weight of the left stone. If there are no stones left, return 0.



1 <= stones.length <= 30
1 <= stones[i] <= 100

</p>



## Examples Test Cases [Leetcode 1049](https://leetcode.com/problems/last-stone-weight-ii/)


<br>
Example1:
<br>

```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0, so the array converts to [1], then that's the optimal value.
```





## Problem Solution [Leetcode 1049](https://leetcode.com/problems/last-stone-weight-ii/)

```cpp
class Solution {
public:

    int f[3030];
    
    int lastStoneWeightII(vector<int>& stones) {
        int n = stones.size();
        int sum = 0;
        for(int s : stones) sum += s;
        memset(f, 0, sizeof f);
        f[0] = 1;
        // 0-1 Knapsack
        for(int i = 0; i < stones.size(); i++){
            for(int j = sum / 2; j >= stones[i]; j--){
                f[j] = f[j] or f[j - stones[i]];
            }
        }
        int max_reach = 0;
        for(int i = sum / 2; i >= 0; i--){
            if(f[i]){
                max_reach = i;
                break;
            }
        }
        return sum - max_reach * 2;
    }
};

```


## Problem Remark 
- 0-1 Knapsack
- The largest subset sum that we want to have without overflowing the sum / 2
- The answer is sum - max_reach
