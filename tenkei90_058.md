---
tags:
    - ダブリング
---

# 典型90-058

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bf)

## 考察

愚直に考えると、処理が行われた後の数字を1回1回シミュレーションによって求めることで解が得られるが、この問題の制約では厳しい。
しかし、3番目の処理で更新されるzは、10^5よりも小さいため、処理を繰り返すと10^5回以内で必ず元の数字に戻ることから、周期性を利用すれば効率的に解を得ることができることに気づける。周期性を利用した解法には、ダブリングがある。

## 計算量

ダブリング：O(logK)
よって、総計算量は
O(logK)

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

int f(int x)
{
    int ret = 0;
    while (x) {
        ret += x % 10;
        x /= 10;
    }
    return ret;
}

int g(int x, int y)
{
    return (x + y) % 100000;
}

int main()
{
    int n;
    ll k;
    cin >> n >> k;

    int d[61][100000];
    rep(i, 100000) {
        int t = g(i, f(i));
        d[0][i] = t;
    }

    for (int i = 1; i < 61; i++) {
        rep(j, 100000) {
            d[i][j] = d[i - 1][d[i - 1][j]];
        }
    }

    int ans = n;
    for (int i = 60; i >= 0; i--) {
        if (k >= 1ll << i) {
            ans = d[i][ans];
            k -= 1ll << i;
        }
    }

    cout << ans << endl;

    return 0;
}
```
