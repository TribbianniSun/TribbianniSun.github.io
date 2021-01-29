# OJ Practice 3


OJ Practice 3, share my solution for these three OJ problems.
<!--more-->

[NCPC 2011 Problem B: Mega Inversion](https://nordic.icpc.io/ncpc2011/ncpc2011problems.pdf)

```cpp
using namespace std;
#define ll long long
#define setval(a, val) memset(a, val, sizeof(a))
#define fastIO                        \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0)
#define INF 1e12

//Definition for a binary tree node.
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
    const int N = 2 * 1e5 + 10;
    const int origin = 1e5 + 10;
public:
    vector<ll> countLarger(vector<int>& nums){
        vector<ll> segtree(2 * N + 2, 0);
        reverse(nums.begin(), nums.end());
        for(int i = 0; i < nums.size(); ++i){
            nums[i] = -nums[i];
        }
        vector<ll> result;
        
        for (int i = nums.size()-1; i >= 0; i--) {
            result.push_back(rangeQuery(segtree, origin + nums[i]));
            update(segtree, origin + nums[i]);
        }

        return result;
    }
    vector<ll> countSmaller(vector<int>& nums) {
        vector<ll> segtree(2*N + 2, 0);
        vector<ll> result;
        for (int i = nums.size()-1; i >= 0; i--) {
            result.push_back(rangeQuery(segtree, origin + nums[i]));
            update(segtree, origin + nums[i]);
        }
        // need to reverse result
        reverse(result.begin(), result.end());
        return result;
    }
    
    void update(vector<ll>& segtree, int index) {
        for (index += N; index > 0; index >>= 1) {
            segtree[index]++;
        }
    }
    
    ll rangeQuery(vector<ll>& segtree, int entry) {
        int left = 0;
        int right = entry;
        ll result = 0;
        for (left += N, right += N; left < right; left >>= 1, right >>= 1) {
            if(entry == 6 + origin){
            }
            if (left%2 == 1) result += segtree[left++];
            if (right%2 == 1) result += segtree[--right];
        }
        return result;
    }    
};

int main()
{

    Solution s;
    int n;
    cin >> n;
    vector<int> nums;
    int t;
    for(int i = 0; i < n; i++){
        cin >> t;
        nums.push_back(t);
    }
    
    vector<ll> smaller = s.countSmaller(nums);
    vector<ll> larger = s.countLarger(nums);

    ll ret = 0;

    for(int i = 0; i < larger.size(); i ++){
        ret += (larger[i] * smaller[i]);
    }
    cout << ret;
    return 0;
}
```
