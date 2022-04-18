---
tags:
    - 整数論
    - 等差数列の和
---

# 典型90-082

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_cd)

## 考察

愚直に考えると、整数を実際に並べて桁数を数えれば解を得ることができるが、この問題の制約では厳しい。各桁の並びにおいて、(桁数) * (等差数列の和)として計算することで、効率よく解を得ることができる。

## 計算量

桁数の取得：O(logR)
よって、総計算量は
O(logR)

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

int digit(ll n)
{
    int ret = 0;
    while (n) {
        n /= 10;
        ret++;
    }
    return ret;
}

mint f(int digit)
{
    mint ret = 1;
    digit--;
    while (digit--) {
        ret *= 10;
    }
    return ret;
}

int main()
{
    ll l, r;
    cin >> l >> r;

    mint ans = 0;
    if (digit(l) == digit(r)) {
        ans += ((mint)l + (mint)r) * ((mint)r - (mint)l + 1) / 2 * digit(l);
    } else {
        int t = digit(r) - digit(l) - 1;
        ans += (f(digit(r)) + (mint)r) * ((mint)r - f(digit(r)) + 1) / 2 * digit(r);
        ans += ((mint)l + f(digit(l) + 1) - 1) * (f(digit(l) + 1) - 1 - (mint)l + 1) / 2 * digit(l);
        rep(i, t) {
            mint A = f(digit(l) + i + 1);
            mint L = f(digit(l) + i + 2) - 1;
            ans += (A + L) * (L - A + 1) / 2 * (digit(l) + i + 1);
        }
    }

    cout << ans << endl;

    return 0;
}
```
