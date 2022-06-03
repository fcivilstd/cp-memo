---
tags:
    - グラフ理論
    - 木
---

# ABC126-D

[問題](https://atcoder.jp/contests/abc126/tasks/abc126_d)

## 考察

木上の二点間距離は、根から頂点iまでの距離をdi、最小共通祖先をwとすると、
du + dv - 2 \* dw
と表すことができる。したがって、根からの距離が偶数の頂点を黒、奇数の頂点を白などと置くとよい。

別の考え方として、長さが奇数の辺で結ばれた頂点同士は絶対に異なる色、長さが偶数の辺で結ばれた頂点同士は同じ色になるという条件を用いると、二点の関係だけから色を決定することができる。

## 計算量

DFS：O(N)
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

int n;
vector<int> ans;
vector<vector<pair<int, int>>> g;

void dfs(int v, int p)
{
    for (auto [t, w] : g[v]) {
        if (t == p) continue;
        if (w & 1) {
            ans[t] = 1 - ans[v];
        } else {
            ans[t] = ans[v];
        }
        dfs(t, v);
    }
}

int main()
{
    cin >> n;

    ans.resize(n);
    g.resize(n);
    rep(i, n - 1) {
        int u, v, w;
        cin >> u >> v >> w;
        u--; v--;

        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }

    ans[0] = 0;
    dfs(0, -1);

    rep(i, n) cout << ans[i] << endl;

    return 0;
}
```
