---
tags:
    - グラフ理論
    - 状態をBFS
---

# ABC132-E

[問題](https://atcoder.jp/contests/abc132/tasks/abc132_e)

## 考察

問題を言い換えると、始点からの距離を3で割った余りが0になる最短経路を求める問題。3で割った余りを状態としてもちながら各頂点をBFSすればよい。

## 計算量

BFS：O(N)
よって、総計算量は
O(N)

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

int main()
{
    int n, m;
    cin >> n >> m;

    vvi to(n);
    rep(i, m) {
        int a, b;
        cin >> a >> b;
        a--; b--;

        to[a].push_back(b);
    }

    int S, T;
    cin >> S >> T;
    S--; T--;

    vvi dist(n, vi(3, INF));
    queue<pii> q;
    dist[S][0] = 0;
    q.push({S, 0});

    while (q.size()) {
        auto [v, l] = q.front(); q.pop();
        for (auto t : to[v]) {
            int tl = (l + 1) % 3;
            if (chmin(dist[t][tl], dist[v][l] + 1)) q.push({t, tl});
        }
    }

    if (dist[T][0] != INF) cout << dist[T][0] / 3 << endl;
    else cout << -1 << endl;

    return 0;
}
```
