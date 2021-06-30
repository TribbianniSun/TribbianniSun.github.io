# Leetcode_946 Lowest Common Ancestor of a Binary Tree



New **stack** to solve Leetcode 946 - Lowest Common Ancestor of a Binary Tree
<!--more-->


## Problem Description [Leetcode 946](https://leetcode.com/problems/validate-stack-sequences/)

<p>
Given two sequences pushed and popped with distinct values, return true if and only if this could have been the result of a sequence of push and pop operations on an initially empty stack.
</p>
 

## Example Test Cases [Leetcode 946](https://leetcode.com/problems/validate-stack-sequences/)

```
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true
Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

```
Input: pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
Output: false
Explanation: 1 cannot be popped before 2.
```


## Problem Solution [Leetcode 946](https://leetcode.com/problems/validate-stack-sequences/)

```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        unordered_set<int> mySet;
        stack<int> myStack;
        int n = popped.size();
        int j = 0;
        for(int i = 0; i < popped.size(); i++){
            int val = popped[i];
            while(!mySet.count(val) and j < n){
                myStack.push(pushed[j]);
                mySet.insert(pushed[j]);
                j += 1;
            }
            if(val != myStack.top()) 
            {
                cout << val;
                return false;
            }
            myStack.pop();
        }
        return true;
    }
};
```
### A quick improvement 
Actually, this is quite dumb; The new value only have two options to make this sequence valid
- in future pushed
- at the top of stack

After considering this clearly, we can write the following code

```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> myStack;
        int n = popped.size();
        int j = 0;
        for(int i = 0; i < popped.size(); i++){
            int val = popped[i];
            if(myStack.size() and myStack.top() == val){
                myStack.pop();
                continue;
            }
            while((myStack.size() == 0 or myStack.top() != val) and j < n){
                myStack.push(pushed[j]);
                j += 1;
            }
            if(val != myStack.top()) 
            {
                return false;
            }
            myStack.pop();
        }
        return true;
    }
};
```
