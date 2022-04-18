---
tags:
    - ランレングス圧縮
    - 累積和
    - 余事象
---

# 典型90-084

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_cf)

## 考察

oとxが並ぶ数で数列を作った場合、任意の2項の積の和が解となる。例えば、
ooxo
の場合、数列に直すと
2 1 1
となり、任意の2項の積の和は、
2 \* 1 + 2 \* 1 + 1 \* 1
で求められる。文字列を数列に直すためにはランレングス圧縮を使用すればよく、任意の2項の積の和を求めるには、累積和を使用して、
2 \* (1 + 1) + 1 * 1
を計算すればよい。また、任意の2項の積の和は、余事象を使用して求められる。

## 計算量

ランレングス圧縮：O(N)
累積和の構築：O(N)
よって、総計算量は
O(N)

## コーディング

累積和

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

int main()
{
    int n;
    string s;
    cin >> n >> s;

    vector<int> rle;
    char pre = 'a';
    rep(i, n) {
        if (s[i] == pre) {
            rle.back()++;
        } else {
            rle.push_back(1);
        }
        pre = s[i];
    }

    vector<int> sum(rle.size() + 1);
    rep(i, rle.size()) {
        sum[i + 1] = sum[i] + rle[i];
    }

    ll ans = 0;
    rep(i, rle.size() - 1) {
        ans += (ll)rle[i] * (sum.back() - sum[i + 1]);
    }
    cout << ans << endl;

    return 0;
}
```

余事象

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

int main()
{
    int n;
    string s;
    cin >> n >> s;

    vector<int> rle;
    char pre = 'a';
    rep(i, n) {
        if (s[i] == pre) {
            rle.back()++;
        } else {
            rle.push_back(1);
        }
        pre = s[i];
    }

    ll ans = (ll)n * (n + 1) / 2;
    rep(i, rle.size()) {
        ans -= (ll)rle[i] * (rle[i] + 1) / 2;
    }
    cout << ans << endl;

    return 0;
}
```
