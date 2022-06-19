---
tags:
    - SCC
---

# 典型90-021

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_u)

## 考察

## 計算量

O(N + M)

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

vi visited;
vvi to, rto;
vi ord;
vvi group;

void dfs(int v)
{
    visited[v] = 1;
    for (auto t : to[v]) {
        if (visited[t]) continue;
        dfs(t);
    }
    ord.push_back(v);
}

void rdfs(int v)
{
    visited[v] = 1;
    group.back().push_back(v);
    for (auto t : rto[v]) {
        if (visited[t]) continue;
        rdfs(t);
    }
}

int main()
{
    int n, m;
    cin >> n >> m;

    visited.resize(n);
    to.resize(n);
    rto.resize(n);

    rep(i, m) {
        int a, b;
        cin >> a >> b;
        a--; b--;
        to[a].push_back(b);
        rto[b].push_back(a);
    }

    rep(i, n) {
        if (visited[i]) continue;
        dfs(i);
    }

    rep(i, n) visited[i] = 0;
    reverse(all(ord));

    ll ans = 0;
    for (auto v : ord) {
        if (visited[v]) continue;
        group.push_back(vi(0));
        rdfs(v);

        int cnt = group.back().size();
        ans += (ll)cnt * (cnt - 1) / 2;
    }

    cout << ans << endl;

    return 0;
}
```
