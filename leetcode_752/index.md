# Leetcode_752 Open the Lock



<!--more-->


## Problem Description [Leetcode 752](https://leetcode.com/problems/open-the-lock/)

<p>
You have a lock in front of you with 4 circular wheels. Each wheel has 10 slots: '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'. The wheels can rotate freely and wrap around: for example we can turn '9' to be '0', or '0' to be '9'. Each move consists of turning one wheel one slot.

The lock initially starts at '0000', a string representing the state of the 4 wheels.

You are given a list of deadends dead ends, meaning if the lock displays any of these codes, the wheels of the lock will stop turning and you will be unable to open it.

Given a target representing the value of the wheels that will unlock the lock, return the minimum total number of turns required to open the lock, or -1 if it is impossible.
</p>

## Example Test Cases [Leetcode 752](https://leetcode.com/problems/open-the-lock/)

```
Input: deadends = ["0201","0101","0102","1212","2002"], target = "0202"
Output: 6
Explanation:
A sequence of valid moves would be "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202".
Note that a sequence like "0000" -> "0001" -> "0002" -> "0102" -> "0202" would be invalid,
because the wheels of the lock become stuck after the display becomes the dead end "0102".
```


## Problem Solution [Leetcode 752](https://leetcode.com/problems/open-the-lock/)
```cpp
class Solution {
public:
    
    int openLock(vector<string>& deadends, string target) {
        unordered_set<string> seen;
        unordered_set<string> deadlock(deadends.begin(), deadends.end());
        int steps = 0;
        queue<string> q;
        q.push("0000");
        while(q.size()){
            int s = q.size();
            for(int i = 0; i < s; i++){
                string c = q.front(); q.pop();
                if(seen.find(c) != seen.end()) continue;
                if(deadlock.find(c) != deadlock.end()) continue;
                seen.insert(c);
                if(c == target) return steps;
                else{
                    for(int i = 0; i < 4; i++){
                        string t = c;
                        int cur = c[i] - '0';
                        t[i] = (cur + 1) % 10 + '0';
                        q.push(t);
                        t[i] = (cur - 1 + 10) % 10 + '0';
                        q.push(t);
                    }
                }
            }
            steps += 1;
        }
        return -1;
    }
};
```
