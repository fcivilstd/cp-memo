---
tags:
    - 数え上げ
    - 重複順列
---

# ABC156-E

[問題](https://atcoder.jp/contests/abc156/tasks/abc156_e)

## 考察

ある状態になるまでに必要な最小の移動回数は、0人になった部屋数である。
この部屋数がK以下である場合の数を全探索すればよい。また、部屋はN部屋しかないため、Kはmin(K, N - 1)で十分である。

1人以上を部屋に割り当てることを考えると重複順列が使えなくなるため、0人以上に修正する。
このとき、人数の総和がN-(N - i)となればよい。ただし、iは0人の部屋数。

## 計算量

組み合わせの前計算：O(N)
K以下全探索：O(min(K, N))

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

struct Combination {
    const int MAX_N = 1001001;
    vector<mint> f, invf;
    Combination() {
        f.resize(MAX_N);
        invf.resize(MAX_N);
        f[0] = 1;
        for (int i = 1; i <= MAX_N; i++) f[i] = f[i - 1] * i;
        invf[MAX_N] = f[MAX_N].inv();
        for (int i = MAX_N; i >= 1; i--) invf[i - 1] = invf[i] * i;
    }
    mint choose(int n, int k)
    {
        if (k < 0 || k > n) return 0;
        return f[n] * invf[k] * invf[n - k];
    }
};

int main()
{
    int n, k;
    cin >> n >> k;
    k = min(k, n - 1);

    mint ans = 0;
    Combination comb;
    rep(i, k + 1) ans += comb.choose(n, i) * comb.choose(n - i - 1 + i, i);

    cout << ans << endl;

    return 0;
}
```
