---
tags:
    - 排他的論理和
---

# ABC171-E

[問題](https://atcoder.jp/contests/abc171/submissions/32273731)

## 考察

偶数回同じ値の排他的論理和をとると0になる。この性質を用いれば、与えられたすべての整数の排他的論理和をとった値とaiの排他的論理和をとると、求めるiの整数が得られる。

## 計算量

すべての整数の排他的論理和：O(N)
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

int main()
{
    int n;
    cin >> n;

    vi a(n);
    rep(i, n) cin >> a[i];

    int tot = 0;
    rep(i, n) tot ^= a[i];

    vi ans(n);
    rep(i, n) ans[i] = tot ^ a[i];

    rep(i, n) cout << ans[i] << " \n"[i == n - 1];

    return 0;
}
```
