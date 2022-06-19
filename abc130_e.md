---
tags:
    - LCS
    - 動的計画法
    - 数え上げ
    - 二次元累積和
---

# ABC130-E

[問題](https://atcoder.jp/contests/abc130/tasks/abc130_e)

## 考察

DP配列を
dp\[i]\[j] := Si、Tjまでみたときの共通部分列の数
と定義する。

遷移は、i、jまでの二次元累積和をsum\[i]\[j]として、
dp\[i]\[j] = sum\[i - 1]\[j - 1] + 1 (Si == Tj)
dp\[i]\[j] = 0 (Si != Tj)
となる。sumを用意しなくても、DP配列を二次元累積和として利用することも可能である。

SiとTjが一致するとき、累積和に1加えた数が共通部分列の数になるのは、これまでの全ての共通部分列の最後に新しい要素を付け加えた共通部分列と、新たな整数だけの共通部分列ができるからである。

例えば、これまでの共通部分列が
()、(1)、(2)、(1, 2)であるとき、新たな整数3が一致すると、
()、(1)、(2)、(1, 2)、(1, 3)、(2, 3)、(1, 2, 3)、(3)

## 計算量

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

const int MOD = 1000000007;
// const int MOD = 998244353;

struct mint {
    ll _x;
    mint() : _x(0) {}
    mint(ll _x) : _x((_x % MOD + MOD) % MOD) {}
    mint& operator++() {_x++; if (_x == MOD) _x = 0; return *this;}
    mint& operator--() {if (_x == 0) _x = MOD; _x--; return *this;}
    mint operator++(int) {mint ret = *this; ++*this; return ret;}
    mint operator--(int) {mint ret = *this; --*this; return ret;}
    mint& operator+=(const mint& a) {if ((_x += a._x) >= MOD) _x -= MOD; return *this;}
    mint& operator-=(const mint& a) {if ((_x += MOD - a._x) >= MOD) _x -= MOD; return *this;}
    mint& operator*=(const mint& a) {_x = _x * a._x % MOD; return *this;}
    mint& operator/=(const mint& a) {_x = _x * a.inv()._x % MOD; return *this;}
    mint operator+(const mint& a) const {return mint(*this) += a;}
    mint operator-(const mint& a) const {return mint(*this) -= a;}
    mint operator*(const mint& a) const {return mint(*this) *= a;}
    mint operator/(const mint& a) const {return mint(*this) /= a;}
    mint pow(ll n) const {
        if (n == 0) return 1;
        mint ret = pow(n / 2);
        ret *= ret;
        return (n & 1) ? ret * _x : ret;
    }
    mint inv() const {return pow(MOD - 2);}
    static mint pow(ll x, ll n) {
        if (n == 0) return 1;
        mint ret = pow(x, n / 2);
        ret *= ret;
        return (n & 1) ? ret * x : ret;
    }
    static mint comb(ll n, int k) {
        if (n - k < k) k = n - k;
        mint a = 1, b = 1;
        rep(i, k) {a *= n - i; b *= i + 1;}
        return a / b;
    }
    bool operator<(const mint& a) const {return _x < a._x;}
    bool operator<=(const mint& a) const {return _x <= a._x;}
    bool operator>(const mint& a) const {return _x > a._x;}
    bool operator>=(const mint& a) const {return _x >= a._x;}
    bool operator==(const mint& a) const {return _x == a._x;}
    bool operator!=(const mint& a) const {return _x != a._x;}
};
istream& operator>>(istream& i, mint& a) {i >> a._x; return i;}
ostream& operator<<(ostream& o, const mint& a) {o << a._x; return o;}

int main()
{
    int n, m;
    cin >> n >> m;

    vi s(n), t(m);
    rep(i, n) cin >> s[i];
    rep(i, m) cin >> t[i];

    vector<vector<mint>> dp(n + 1, vector<mint>(m + 1));
    dp[0][0] = 1;

    rep(i, n + 1) rep(j, m + 1) {
        if (i > 0 && j > 0 && s[i - 1] == t[j - 1]) dp[i][j] += dp[i - 1][j - 1];
        if (i > 0) dp[i][j] += dp[i - 1][j];
        if (j > 0) dp[i][j] += dp[i][j - 1];
        if (i > 0 && j > 0) dp[i][j] -= dp[i - 1][j - 1];
    }

    cout << dp[n][m] << endl;

    return 0;
}
```
