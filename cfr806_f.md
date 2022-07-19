---
tags:
    - 平面走査
    - BIT
---

# Codeforces Round #806-F

[問題](https://codeforces.com/contest/1703/problem/F)

## 考察

ある軸を端から順に走査することで、あるタイミングの状態から求めたい値を高速に求めるという手法が平面走査。

この問題では、配列を後ろから走査しながら、ある値以上の値が登場した回数を区間和で数えればよい。

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

// const int MOD = 1000000007;
// const int MOD = 998244353;

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
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        BIT<int> bit(n + 1);

        vi a(n);
        rep(i, n) cin >> a[i], a[i]++;

        ll ans = 0;
        rrng(i, 0, n) {
            if (a[i] >= i + 2) continue;
            bit.add(a[i], 1);
            ans += bit.sum(n + 1) - bit.sum(i + 2);
        }

        cout << ans << endl;
    }

    return 0;
}
```
