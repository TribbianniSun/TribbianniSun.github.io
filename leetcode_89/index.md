# Leetcode_89 Gray Code



Use **dp** to solve Leetcode 89 - Gray Code.
<!--more-->

## Problem Description [Leetcode 89](https://leetcode.com/problems/gray-code/)

<p>
An n-bit gray code sequence is a sequence of 2n integers where:

Every integer is in the inclusive range [0, 2n - 1],
The first integer is 0,
An integer appears no more than once in the sequence,
The binary representation of every pair of adjacent integers differs by exactly one bit, and
The binary representation of the first and last integers differs by exactly one bit.
Given an integer n, return any valid n-bit gray code sequence.
</p>


## Example Test Cases [Leetcode 89](https://leetcode.com/problems/gray-code/)



```

Input: n = 2
Output: [0,1,3,2]
Explanation:
The binary representation of [0,1,3,2] is [00,01,11,10].
- 00 and 01 differ by one bit
- 01 and 11 differ by one bit
- 11 and 10 differ by one bit
- 10 and 00 differ by one bit
[0,2,3,1] is also a valid gray code sequence, whose binary representation is [00,10,11,01].
- 00 and 10 differ by one bit
- 10 and 11 differ by one bit
- 11 and 01 differ by one bit
- 01 and 00 differ by one bit
```


## Problem Solution [Leetcode 89](https://leetcode.com/problems/gray-code/)

```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> ret = {0, 1};
        for(int i = 1; i < n; i++){
            vector<int> back;
            for(int j = 0; j < ret.size(); j++){
                back.push_back(ret[j] + (0 << i));
            }
            for(int j = ret.size() - 1; j >= 0; j--){
                back.push_back(ret[j] + (1 << i));
            }
            ret = back;
        }
        return ret;
    }
};
// 0, 1
// 00, 01, 11, 10
// 000, 001, 011, 010, 110, 111, 101, 100
//
```


