# Leetcode_307 Range Sum Query - Mutable



Use **SegmentTree** to solve Leetcode 307 Range Sum Query - Mutable.
<!--more-->


## Problem Solution [Leetcode 307](https://leetcode.com/problems/range-sum-query-mutable/)
```cpp
class NumArray {
public:
    int n;
    struct Node{
        int l, r;
        int sum;
    }tr[3 * 10005 * 4];
    
    void pushup(int u){
        tr[u].sum = tr[u << 1].sum + tr[u << 1 | 1].sum;    
    }
    
    void build(int u, int l, int r){
        tr[u].l = l, tr[u].r = r;
        if(l == r) return;
        int mid = (tr[u].l + tr[u].r) / 2;
        build(u << 1, l, mid);
        build(u << 1 | 1, mid + 1, r);
    }
    
    void update(int u, int x, int v){
        if(tr[u].l == x and tr[u].r == x) {
            tr[u].sum = v;
            return;
        }
        else{
            int mid = (tr[u].l + tr[u].r) / 2;
            if(x <= mid) update(u << 1, x, v);
            else update(u << 1 | 1, x, v);
            pushup(u);
        }
    }
    
    int query(int u, int l, int r){
        if(tr[u].l >= l and tr[u].r <= r) return tr[u].sum;
        int mid = (tr[u].l + tr[u].r) / 2;
        int v = 0;
        if(l <= mid) v = query(u << 1, l, r);
        if(r > mid) v += query(u << 1 | 1, l , r);
        return v;
    }
    
    
    NumArray(vector<int>& nums) {
        memset(tr, 0, sizeof tr);
        n = nums.size();
        build(1, 1, n);
        for(int i  = 0; i < nums.size(); i++){
            update(1, i + 1, nums[i]);
        }
    }
    
    void update(int index, int val) {
        update(1, index + 1, val);
    }
    
    int sumRange(int left, int right) {
        return query(1, left + 1, right + 1);
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * obj->update(index,val);
 * int param_2 = obj->sumRange(left,right);
 */
```
