---
tags:
    - トポロジカルソート
---

# AOJ-Topological Sort

[問題](https://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_4_B)

## 考察

## 計算量

O(V + E)(ただし、Vは頂点数、Eは辺数)

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

int main()
{
    int n, m;
    cin >> n >> m;

    vector<int> in(n);
    vector<vector<int>> to(n);
    rep(i, m) {
        int a, b;
        cin >> a >> b;
        a--; b--;

        in[b]++;
        to[a].push_back(b);
    }

    queue<int> q;
    rep(i, n) if (in[i] == 0) q.push(i);

    vector<int> ans;
    while (q.size()) {
        int v = q.front(); q.pop();
        ans.push_back(v);

        for (auto t : to[v]) {
            in[t]--;
            if (in[t] == 0) q.push(t);
        }
    }

    rep(i, ans.size()) cout << ans[i] << endl;

    return 0;
}
```
