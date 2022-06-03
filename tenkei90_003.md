---
tags:
    - グラフ理論
    - 木
    - 木の直径
---

# 典型90-003

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_c)

## 考察

求めたいのは木における2頂点間の最大距離である。
愚直に考えると、1からNまでの頂点をそれぞれ根としたときに最も深い頂点を求め、最大値を求めることで解を得ることができる。しかし、計算量がO(N^2)となり、この問題の制約では厳しい。
木における2頂点間の最大距離とは言い換えると木の直径であるため、木の直径を求めれば良いことに気づける。

## 計算量

木の直径を求める：O(N)
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

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

int n;
vector<vector<int>> to;
vector<int> dist;

void dfs(int d, int v, int p)
{
    dist[v] = d;
    for (auto& t : to[v]) {
        if (t == p) continue;
        dfs(d + 1, t, v);
    }
}

int main()
{
    cin >> n;
    to.resize(n);
    dist.resize(n);
    
    rep(i, n - 1) {
        int a, b;
        cin >> a >> b;
        a--; b--;
        to[a].push_back(b);
        to[b].push_back(a);
    }

    dfs(0, 0, -1);

    int mx = 0;
    int u = -1;
    rep(i, dist.size()) {
        if (chmax(mx, dist[i])) {
            u = i;
        }
    }

    dfs(0, u, -1);

    int uv = 0;
    rep(i, dist.size()) {
        chmax(uv, dist[i]);
    }

    cout << uv + 1 << endl;

    return 0;
}
```
