# OJ Practice 2




OJ Practice 2, share my solution for these three OJ problems.
<!--more-->


[Robots on a grid](https://www.e-olymp.com/en/problems/6020)

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

class Solution
{
public:
    int test()
    {
    }
};

int solve(vector<vector<int>>& board){
    
    int m = board.size(), n = board[0].size();
    int step = 0;
    vector<int> dirs = {0, 1, 0, -1, 0};
    set<int> seen;
    deque<int> q;
    
    q.push_back(0);
    seen.insert(0);


    while(q.size()){
        int size = q.size();
        for(int i = 0; i < size; i++){
            int p = q.front();
            q.pop_front();
            int r = p / n, c = p % n;
            if(r == m - 1 && c == n - 1){
                return step;
            }
            else{
                for(int i = 0; i < 4; i++){
                    int nr = r + (board[r][c] * dirs[i]), nc = c + (board[r][c] * dirs[i + 1]);
                    if(nr >= 0 && nr < m && nc >= 0 && nc < n){
                        int np = nr * n + nc;
                        if(seen.find(np) == seen.end()){
                            seen.insert(np);
                            q.push_back(np);
                        }
                    }
                }
            }
        }
        step += 1;
    }
    return -1;


}
int main()
{

    int m, n;
    cin >> m >> n;
    vector<vector<int>> board(m, vector<int>(n, 0));
    char c;
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            cin >> c;
            board[i][j] = c - '0';
        }
    }
    // for(int i = 0; i < m; i++){
    //     for(int j = 0; j < n; j++){
    //         cout << board[i][j];
    //     }
    // }
    cout << solve(board);
    return 0;
}
```


[SERGRID - Grid](https://www.spoj.com/problems/SERGRID/)

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

int solve(vector<vector<unsigned int>>& board){
    int n = board.size() - 1;
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            if(board[i][j] == -1){
                board[i][j] = 0;
            }
            else{
                board[i][j] = (board[i][j - 1] % 0x7FFFFFFF + board[i - 1][j] % 0x7FFFFFFF) % 0x7FFFFFFF;
            }
        }
    }
    return board[n][n];
}

bool isValid(vector<vector<int>>& board){
    int n = board.size();

    // invalid board
    if(board[0][0] == -1){
        return false;
    }

    vector<int> dirs = {0, 1, 0, -1, 0};
    // r * n + c
    set<int> seen;
    deque<int> d;
    seen.insert(0);
    d.push_back(0);
    while(d.size()){
        int p = d.front();
        d.pop_front();
        int r = p / n, c = p % n;
        if(r == n - 1 && c == n - 1){
            return true;
        }
        else{
            for(int i = 0; i < dirs.size() - 1; i++){
                int nr = r + dirs[i], nc = c + dirs[i + 1];
                if(nr >= 0 && nr < n && nc >= 0 && nc < n && board[nr][nc] == 0){
                    int np = nr * n + nc;
                    if(seen.find(np) == seen.end()){
                        seen.insert(np);
                        d.push_back(np);
                    }
                }
            }
        }
    }
    return false;



}

int main()
{
    int n;
    char c;
    cin >> n;
    vector<vector<int>> validBoard(n, vector<int>(n, 0));
    vector<vector<unsigned int>> board(n + 1, vector<unsigned int>(n + 1, 0));

    for(int i = 0; i < n; i++){
        for(int j = 0; j < n; j++){
            cin >> c;
            if(c == '.'){
                board[i + 1][j + 1] = 0;
                validBoard[i][j] = 0;
            }
            else{
                board[i + 1][j + 1] = -1;
                validBoard[i][j] = -1;
            }
        }
    }
    
    if(isValid(validBoard) == false){
        cout << "INCONCEIVABLE";
        return 0;
    }

    board[0][1] = 1;
    int ret = solve(board);

    if (ret != 0){
        cout << ret;
    }
    else{
        if(isValid(validBoard) == false){
            cout << "INCONCEIVABLE";
            return 0;
        }
        else{
            cout << "THE GAME IS A LIE";
        }
    }


    return 0;
}


```
