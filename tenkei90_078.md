---
tags:
    - グラフ理論
---

# 典型0-078

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bz)

## 考察

辺の制約が緩いため、各頂点について辺を全探索して条件を満たすものを数えれば良い。

## 計算量

辺の全探索：O(M)
よって、総計算量は
O(M)

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

    vector<vector<int>> to(n);
    rep(i, m) {
        int a, b;
        cin >> a >> b;
        a--; b--;
        to[a].push_back(b);
        to[b].push_back(a);
    }

    int ans = 0;
    rep(i, n) {
        int cnt = 0;
        for (auto t : to[i]) {
            if (t < i) cnt++;
        }
        if (cnt == 1) ans++;
    }

    cout << ans << endl;

    return 0;
}
```
