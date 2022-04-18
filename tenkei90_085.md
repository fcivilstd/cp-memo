---
tags:
    - 約数全列挙
---

# 典型90-085

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_cg)

## 考察

約数を全列挙し、3つの積がKになる組み合わせを全探索で数えれば良い。
Kの約数をd(K)とすると、
10^6以下の場合K = 720,720で最大値d(K) = 240
10^9以下の場合K = 735,134,400で最大値d(K) = 1,344
10^12以下の場合K = 963,761,198 400で最大値d(K) = 6,720
10^18以下の場合K = 897,612,484,786,717,600で最大値d(K) = 103,680

## 計算量

約数全列挙：O(√K)
よって、総計算量は
O(√K)

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
    ll k;
    cin >> k;

    vector<ll> a, b;
    for (ll i = 1; i * i <= k; i++) {
        if (k % i == 0) {
            a.push_back(i);
            if (i * i != k) b.push_back(k / i);
        }
    }
    reverse(all(b));
    rep(i, b.size()) a.push_back(b[i]);

    ll ans = 0;
    for (int i = 0; i < a.size(); i++) {
        for (int j = i; j < a.size(); j++) {
            if ((k / a[i]) % a[j] == 0 && a[j] <= k / a[i] / a[j]) {
                ans++;
            }
        }
    }

    cout << ans << endl;

    return 0;
}
```
