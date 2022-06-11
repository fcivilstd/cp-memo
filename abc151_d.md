---
tags:
    - BFS
---

# ABC141-D

[問題](https://atcoder.jp/contests/abc141/tasks/abc141_d)

## 考察

全2点対に対する最短経路の最大値を求めればよい。計算量をさらに落とす工夫として、全始点に対する最長経路の最大値を求めてもよい。

## 計算量

BFS：O(HW)
よって、総計算量は、
O((HW)^3)、O((HW)^2)

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
using vi = vector<int>;
using vvi = vector<vector<int>>;
using pii = pair<int, int>;

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

const int INF = 1001001001;

int h, w;
vector<string> grid;
int dx[] = {0, 1, 0, -1};
int dy[] = {1, 0, -1, 0};

int bfs(int s, int g)
{
    vvi dist(h, vi(w, INF));
    int sx = s / w, gx = g / w;
    int sy = s - w * sx, gy = g - w * gx;

    if (grid[sx][sy] != '.' || grid[gx][gy] != '.') return -1;
    queue<pii> q;
    q.push({sx, sy});
    dist[sx][sy] = 0;

    while (q.size()) {
        auto [nx, ny] = q.front(); q.pop();
        if (nx == gx && ny == gy) return dist[nx][ny];

        rep(k, 4) {
            int tx = nx + dx[k];
            int ty = ny + dy[k];

            if (tx < 0 || tx >= h || ty < 0 || ty >= w) continue;
            if (grid[tx][ty] != '.') continue;
            if (dist[tx][ty] <= dist[nx][ny] + 1) continue;

            q.push({tx, ty});
            dist[tx][ty] = dist[nx][ny] + 1;
        }
    }

    return -1;
}

int main()
{
    cin >> h >> w;

    grid.resize(h);
    rep(i, h) cin >> grid[i];

    int ans = -1;
    rep(j, h * w) rep(i, j) {
        chmax(ans, bfs(i, j));
    }

    cout << ans << endl;

    return 0;
}
```
