---
tags:
    - メモ化再帰
    - 動的計画法
    - 倍数の性質
---

# 典型0-042

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ap)

## 考察

9の倍数かどうかは、各桁の和が9の倍数であるかで判定できる。
Xは各桁の和がKである必要があるため、Xが9の倍数でなければ解は0である。
各桁の和がKである正の整数の数は、動的計画法で求められる。

dp(i, j, m) := i桁目がjで、各桁の和がmである正の整数の数
仮にこのようなDP配列を考えた場合、最大の桁数はKであるため、計算量はO(K^2)となり、この問題の制約では厳しい。

考察を進めると、各桁の和がKになるためには、DP配列の遷移として、
dp[k] += dp[k - i] (i = 1...9)
となっていてほしい。dp[k - i]は最初の段階では求まっていないため、
dp[k - i] += dp[k - i - m] (m = 1...9), dp[k - i - m] += dp[k - i - m - n] (n = 1...9), ..., dp[1] += dp[0 + 1]
のようにdp[0]まで遡る必要がある。つまり、メモ化再帰で解ける構造になっていることに気づける。メモ化再帰ではなく動的計画法で解く場合は、DP配列のインデックスを小さい方から埋めていくと同じ解が得られる。

## 計算量

DP配列のインデックスでfor分を回す：O(K)
各桁の値で遷移させる：O(d) (1...9の9パターン)
よって、総計算量は
O(Kd)

## コーディング

メモ化再帰

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

vector<mint> dp;

mint dfs(int x)
{
    for (int i = 1; i <= 9; i++) {
        if (x - i < 0) continue;
        if (dp[x - i] != 0) dp[x] += dp[x - i];
        else dp[x] += dfs(x - i);
    }
    return dp[x];
}

int main()
{
    int k;
    cin >> k;

    if (k % 9 != 0) {
        cout << 0 << endl;
        return 0;
    }

    dp.resize(k + 1);
    dp[0] = 1;

    dfs(k);

    cout << dp[k] << endl;

    return 0;
}

```

動的計画法

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
    int k;
    cin >> k;

    if (k % 9 != 0) {
        cout << 0 << endl;
        return 0;
    }

    mint dp[100100];
    dp[0] = 1;
    for (int i = 1; i <= k; i++) {
        int n = min(i, 9);
        for (int j = 1; j <= n; j++) {
            dp[i] += dp[i - j];
        }
    }

    cout << dp[k] << endl;

    return 0;
}
```
