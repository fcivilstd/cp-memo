---
tags:
    - ダブリング
---

# ABC167-D

[問題](https://atcoder.jp/contests/abc167/tasks/abc167_d)

## 考察

周期性よりダブリングを使用することで十分高速に解を得られる。

## 計算量

ダブリング：O(NlogK)
よって、総計算量は
O(NlogK)

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
    ll k;
    cin >> n >> k;

    vi a(n);
    rep(i, n) cin >> a[i];
    rep(i, n) a[i]--;

    int d[61][200010];
    rep(j, n) d[0][j] = a[j];
    rep(i, 60) rep(j, n) d[i + 1][j] = d[i][d[i][j]];

    int now = 0;
    rrng(i, 0, 61) {
        if (1LL << i <= k) {
            k -= 1LL << i;
            now = d[i][now];
        }
    }

    cout << now + 1 << endl;

    return 0;
}
```
