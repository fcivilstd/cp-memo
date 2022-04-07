---
tags:
    - 貪欲法
---

# 典型90-014

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_n)

## 考察

直線状に並んでいるため、AとBをソートして対応づければ最適になる。
紙に書けば分かるが、対応が交差してしまった場合(A1とB2、A2とB1が対応するなど)は、必ず交差しなかった場合以上の不便さとなる。

## 計算量

ソート：O(NlogN)
対応付け：O(N)
よって、総計算量は
O(NlogN + N)

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
    int n;
    cin >> n;

    vector<int> a(n), b(n);
    rep(i, n) cin >> a[i];
    rep(i, n) cin >> b[i];

    sort(all(a));
    sort(all(b));

    ll ans = 0;
    rep(i, n) {
        ans += abs((ll)a[i] - (ll)b[i]);
    }

    cout << ans << endl;

    return 0;
}
```
