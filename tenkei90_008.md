---
tags:
    - 動的計画法
    - 耳DP
---

# 典型90-008

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_h)

## 考察

愚直に考えると、Sから0個以上の文字を取り出して"atcoder"になっている場合を数えると解が得られるが、この問題の制約では厳しい。
"atcoder"という文字列は、同じ文字が含まれていないため、例えば"at"までを数える場合は、"t"が出てくるたびにそれまでに"a"が出てきた数を"t"のカウントに足しこめば良いと気づける。同様に"atc"までを数える場合は、それまでの"t"のカウントを"c"のカウントに足しこめば良い。

## 計算量

文字列を一文字ずつ確認する：O(N)
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

int f(char c)
{
    if (c == 'a') return 1;
    else if (c == 't') return 2;
    else if (c == 'c') return 3;
    else if (c == 'o') return 4;
    else if (c == 'd') return 5;
    else if (c == 'e') return 6;
    else if (c == 'r') return 7;
    else return -1;
}

int g(char c)
{
    if (c == 'a') return 0;
    else if (c == 't') return 1;
    else if (c == 'c') return 2;
    else if (c == 'o') return 3;
    else if (c == 'd') return 4;
    else if (c == 'e') return 5;
    else if (c == 'r') return 6;
    else return -1;
}

int main()
{
    int n;
    string s;
    cin >> n >> s;

    vector<mint> dp(8);
    dp[0] = 1;

    rep(i, s.size()) {
        if (f(s[i]) != -1) dp[f(s[i])] += dp[g(s[i])];
    }

    cout << dp[7] << endl;

    return 0;
}
```
