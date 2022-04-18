---
tags:
    - 整数論
    - 素因数分解
---

# 典型90-075

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bw)

## 考察

1回の操作で素因数の総数の半分が残るため、素因数分解をして素因数の総数を2で割れる回数を数えれば良い。

## 計算量

素因数分解：O(√N)
よって、総計算量は
O(√N)

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

vector<pair<ll, int>> pf(ll n)
{
    vector<pair<ll, int>> ret;

    for (ll i = 2; i * i <= n; i++) {
        if (n % i) continue;
        int x = 0;
        while (n % i == 0) {
            n /= i;
            x++;
        }
        ret.push_back({i, x});
    }
    if (n != 1) ret.push_back({n, 1});

    return ret;
}

int main()
{
    ll n;
    cin >> n;

    auto p = pf(n);
    int cnt = 0;
    for (auto [x, y] : p) {
        cnt += y;
    }

    int ans = 0;
    while (cnt > 1) {
        cnt = (cnt + 1) / 2;
        ans++;
    }

    cout << ans << endl;

    return 0;
}
```
