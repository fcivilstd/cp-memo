---
tags:
    - N進数
---

# 典型90-067

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bo)

## 考察

N進数の変換を実装するだけ。

## 計算量

操作の繰り返し：O(K)
N進数の変換：O(logN)
よって、総計算量は
O(KlogN)

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

ll p(ll x, int n)
{
    ll ret = 1;
    while (n--) {
        ret *= x;
    }
    return ret;
}

ll to10(string x)
{
    ll ret = 0;
    reverse(all(x));
    rep(i, x.size()) {
        ll t = x[i] - '0';
        ret += t * p(8, i);
    }
    return ret;
}

string to9(ll x)
{
    string ret = "";
    while (x) {
        ll t = x % 9;
        if (t == 8) t = 5;
        ret += t + '0';
        x /= 9;
    }
    reverse(all(ret));
    if (ret != "") return ret;
    else return "0";
}

int main()
{
    string n;
    int k;

    cin >> n >> k;

    string ans = n;
    while (k--) {
        ans = to9(to10(ans));
    }

    cout << ans << endl;

    return 0;
}
```
