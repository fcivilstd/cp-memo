---
tags:
    - 01-BFS
---

# 典型90-043

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_aq)

## 考察

向きを変えなければコストは0、向きを変えればコストは1であるため、01-BFSを使用すれば良いと気づける。
01-BFSは、コスト0となる遷移を優先的に取り出すアルゴリズムであり、ダイクストラ法がpriority_quequeで行っているソートを手動で行っているに過ぎない。

## 計算量

01-BFS：O(HW)
よって、総計算量は
O(HW)

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

int dx[] = {0, 1, 0, -1};
int dy[] = {1, 0, -1, 0};
const int inf = 1 << 30;

int main()
{
    int h, w;
    cin >> h >> w;

    int rs, cs, rt, ct;
    cin >> rs >> cs >> rt >> ct;
    rs--; cs--; rt--; ct--;

    vector<vector<int>> grid(h, vector<int>(w));
    rep(i, h) rep(j, w) {
        char c;
        cin >> c;
        if (c == '#') grid[i][j] = 1;
    }

    vector<vector<vector<int>>> cost(h, vector<vector<int>>(w, vector<int>(4, inf)));
    rep(i, 4) cost[rs][cs][i] = 0;

    // first: dir, second: cost, third: r, fourth: c
    deque<tuple<int, int, int, int>> q;
    rep(i, 4) q.push_front({i, 0, rs, cs});

    while (q.size()) {
        auto [d, c, nr, nc] = q.front(); q.pop_front();
        rep(i, 4) {
            int tr = nr + dx[i];
            int tc = nc + dy[i];
            if (tr < 0 || tr >= h || tc < 0 || tc >= w) continue;
            if (grid[tr][tc]) continue;
            if (i == d) {
                if (chmin(cost[tr][tc][i], c)) q.push_front({i, c, tr, tc});
            } else {
                if (chmin(cost[tr][tc][i], c + 1)) q.push_back({i, c + 1, tr, tc});
            }
        }
    }

    int ans = inf;
    rep(i, 4) chmin(ans, cost[rt][ct][i]);

    cout << ans << endl;

    return 0;
}
```
