---
tags:
    - 動的計画法
    - 累積和
---

# ABC253-E

[問題](https://atcoder.jp/contests/abc253/tasks/abc253_e)

## 考察

i番目にjを採用したときの場合の数はi-1番目で1 ~ j-k、j+k ~ mを採用したときの場合の数の総和である。これを効率的に求めるために、動的計画法と累積和を考えるとよい。

## 計算量

区間和の計算(BITを使用した場合)：O(logM)
動的計画法：O(NM)
よって、総計算量は
O(NMlogM)

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
const int MOD = 998244353;

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

template <class T> struct BIT {
    // _data[0] ... _data[_n]
    int _n;
    vector<T> _data;

    BIT() : _n(0) {}
    BIT(int n) : _n(n), _data(n + 1) {}

    // _data[k] += x
    void add(int k, T x)
    {
        while (k <= _n) {
            _data[k] += T(x);
            k += k & -k;
        }
    }

    // _data[1] + ... + _data[r]
    T sum(int r)
    {
        T ret = 0;
        while (r > 0) {
            ret += _data[r];
            r -= r & -r;
        }
        return ret;
    }
};

int main()
{
    int n, m, k;
    cin >> n >> m >> k;

    vector<mint> dp(m + 1, 1);
    BIT<mint> bit(m);
    rng(i, 1, m + 1) bit.add(i, 1);

    rep(i, n - 1) {
        vector<mint> _dp(m + 1);
        BIT<mint> _bit(m);
        rng(j, 1, m + 1) {
            if (!k) {
                _dp[j] += bit.sum(m);
                continue;
            }

            _dp[j] += bit.sum(m) - bit.sum(min(j + k - 1, m));
            _dp[j] += bit.sum(max(j - k, 0));
        }
        rng(j, 1, m + 1) _bit.add(j, _dp[j]);
        swap(dp, _dp);
        swap(bit, _bit);
    }

    cout << bit.sum(m) << endl;

    return 0;
}
```
