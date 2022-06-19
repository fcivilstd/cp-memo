---
tags:
    - 動的計画法
    - 桁DP
---

# ABC129-E

[問題](https://atcoder.jp/contests/abc129/tasks/abc129_e)

## 考察

桁DPは、大きい方の桁から見て、基準より1回でも小さい値を採用したかどうかのフラグを管理するのが基本。

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

mint dp[100100][2][2];

int main()
{
    string s;
    cin >> s;

    vi bit(s.size());
    rep(i, s.size()) bit[i] = s[i] - '0';

    dp[0][0][0] = 1;
    rep(i, s.size()) {
        // dp[i + 1][][0] += dp[i][][0]
        rep(j, 2) {
            if (bit[i]) dp[i + 1][1][0] += dp[i][j][0] * 2;
            else dp[i + 1][0][0] += dp[i][j][0];
        }

        // dp[i + 1][][1] += dp[i][][0]
        rep(j, 2) if (bit[i]) dp[i + 1][0][1] += dp[i][j][0];

        // dp[i + 1][][1] += dp[i][][1]
        rep(j, 2) {
            dp[i + 1][0][1] += dp[i][j][1];
            dp[i + 1][1][1] += dp[i][j][1] * 2;
        }
    }

    mint ans = 0;
    rep(j, 2) rep(k, 2) ans += dp[s.size()][j][k];
    cout << ans << endl;

    return 0;
}
```
