# Leetcode 786 - K-th Smallest Prime Fraction





New **BFS** to solve Leetcode 786 - K-th Smallest Prime Fraction
<!--more-->



## Problem Description [Leetcode 786](https://leetcode.com/problems/k-th-smallest-prime-fraction/)
<p>
You are given a sorted integer array arr containing 1 and prime numbers, where all the integers of arr are unique. You are also given an integer k.

For every i and j where 0 <= i < j < arr.length, we consider the fraction arr[i] / arr[j].

Return the kth smallest fraction considered. Return your answer as an array of integers of size 2, where answer[0] == arr[i] and answer[1] == arr[j].
 
</p>



## Example Test Cases [Leetcode 786](https://leetcode.com/problems/k-th-smallest-prime-fraction/)


<br>
Example1:
<br>

```
Input: arr = [1,2,3,5], k = 3
Output: [2,5]
Explanation: The fractions to be considered in sorted order are:
1/5, 1/3, 2/5, 1/2, 3/5, and 2/3.
The third fraction is 2/5.
```


## Problem Solution [Leetcode 786](https://leetcode.com/problems/k-th-smallest-prime-fraction/)

```cpp
// BFS
vector<int> global_arr;
class Node
{
    
public:
    int denominator;
    int numerator;
    double val;
    
    Node(int de, int nu){
        this -> denominator = de;
        this -> numerator = nu;
        this -> val = (double)global_arr[nu] / global_arr[de];
    }

};

class Compare
{
public:
    bool operator() (Node& n1, Node& n2)
    {
        return n1.val > n2.val;
    }
};



class Solution {
public:
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        global_arr.clear();
        for(int i : arr){
            global_arr.push_back(i);
        }
        
        
        std::priority_queue<Node, std::vector<Node>, Compare> pq;
        
        for(int i = 1; i < arr.size(); i++){
            Node cur(i, 0);
            pq.push(cur);
        }
        
        for(int i = 0; i < k - 1; ++i){
            // cout << pq.top().numerator << " " << pq.top().denominator << endl;
            Node cur = pq.top();
            pq.pop();
            
            if(cur.numerator == cur.denominator - 1){
                continue;
            }
            else{
                cur.numerator += 1;
                cur.val = (double)global_arr[cur.numerator] / global_arr[cur.denominator];
                pq.push(cur);
            }
        }
        // cout << global_arr[pq.top().numerator] << " " << global_arr[pq.top().denominator];
        vector<int> ret{global_arr[pq.top().numerator], global_arr[pq.top().denominator]};
        return ret;
            
        
    }
};
```

## Problem Remark [Leetcode 786](https://leetcode.com/problems/k-th-smallest-prime-fraction/)
- Using Heap
- O(k * log(n)) solution
