---
tags:
    - グラフ理論
    - 二部グラフ
---

# 典型90-026

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_z)

## 考察

木は二部グラフであるため、深さの偶奇で色分けして隣り合わない頂点を選ぶことができる。N/2個の頂点を選ぶには、深さが偶数、奇数の大きいから選べば良い。

## 計算量

色分けのための深さ優先探索：O(N)
頂点の選択：O(N)
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

void dfs(int v, int p, int d)
{
    dist[v] = d;
    for (auto t : to[v]) {
        if (t == p) continue;
        dfs(t, v, d + 1);
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

    dfs(0, -1, 0);

    int odd = 0, even = 0;
    rep(i, n) {
        if (dist[i] & 1) odd++;
        else even++;
    }

    vector<int> ans;
    for (int i = 0; i < n && ans.size() < n / 2; i++) {
        if (odd >= even && dist[i] % 2 == 1) ans.push_back(i + 1);
        if (odd < even && dist[i] % 2 == 0) ans.push_back(i + 1);
    }

    rep(i, ans.size()) cout << ans[i] << " \n"[i == ans.size() - 1];

    return 0;
}
```
