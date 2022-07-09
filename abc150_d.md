---
tags:
    - 整数論
    - 最小公倍数
    - 奇数の数
---

# ABC150-D

[問題](https://atcoder.jp/contests/abc150/tasks/abc150_d)

## 考察

0.5を含まないように全体に2を掛ける。その後、最小公倍数を求め、最小公倍数をaiで割った結果が奇数であることを確認する。偶数が含まれていれば、Xは存在しない。あとは、最小公倍数を奇数倍できるバリエーションを数えればよい。

K以下の奇数の個数は、
ceil(K / 2) = floor((k + 1) / 2)

## 計算量

最小公倍数を求める：O(Nloga)
よって、総計算量は
O(Nloga)

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

ll LCM(ll x, ll y)
{
    ll g = __gcd(x, y);
    return x * y / g;
}

int main()
{
    int n, m;
    cin >> n >> m;

    vi a(n);
    rep(i, n) cin >> a[i];

    ll lcm = 1;
    rep(i, n) lcm = LCM(lcm, a[i]);

    rep(i, n) {
        if ((lcm / a[i]) % 2 == 0) {
            cout << 0 << endl;
            return 0;
        }
    }

    cout << (2 * m / lcm + 1) / 2 << endl;

    return 0;
}
```
