---
tags:
    - DFS
    - 全探索
    - バックトラック
---

# 典型90-072

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bt)

## 考察

マスの数が少ないため、全探索が可能であると気づける。全探索には、再帰関数によるバックトラックが有効である。

## 計算量

???

## コーディング

```cpp
// #define _GLIBCXX_DEBUG
#include<bits/stdc++.h>

#define rep(i, n) for (int i = 0; i < (int)(n); i++)
#define rng(i, a, b) for (int i = (int)(a); i < (int)(b); i++)
#define rrng(i, a, b) for (int i = (int)(b) - 1; i >= (int)(a); i--)
#define all(x) x.begin(), x.end()
#define rall(x) x.rbegin(), x.rend()

using namespace std;

using ll = long long;
using ull = unsigned long long;

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

int ans = -1;
int h, w;
int dx[] = {0, 1, 0, -1};
int dy[] = {1, 0, -1, 0};
vector<vector<bool>> visited;
vector<string> grid;

void dfs(int x, int y, int cnt, int sx, int sy)
{
    cnt++;
    visited[x][y] = true;
    rep(i, 4) {
        int tx = x + dx[i];
        int ty = y + dy[i];

        if (tx == sx && ty == sy && cnt > 2) {
            chmax(ans, cnt);
            continue;
        }

        if (tx < 0 || tx >= h || ty < 0 || ty >= w) continue;
        else if (visited[tx][ty]) continue;
        else if (grid[tx][ty] == '#') continue;

        dfs(tx, ty, cnt, sx, sy);
    }

    cnt--;
    visited[x][y] = false;
    return;
}

int main()
{
    cin >> h >> w;

    visited.assign(h, vector<bool>(w));
    grid.resize(h);
    rep(i, h) cin >> grid[i];

    rep(i, h) rep(j, w) {
        if (grid[i][j] == '.') dfs(i, j, 0, i, j);
    }

    cout << ans << endl;

    return 0;
}
```
