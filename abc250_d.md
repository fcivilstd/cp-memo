---
tags:
    - エラトステネスの篩
    - 二分探索
---

# ABC250-D

[問題](https://atcoder.jp/contests/abc250/tasks/abc250_d)

## 考察

q <= 10^6 であることから、q以下の素数の全列挙が可能であることが分かる。素数の全列挙は、エラトステネスの篩を使用すればよい。次に、qを決め打ちし、pを探索することを考える。pは
p <= floor(n / q^3)
かつ
p < q
を満たせばよく、また、単調性から二分探索が可能であることに気づける。取りうるpの範囲の内、素数がいくつ含まれるかは、事前に用意している素数のリストを二分探索すれば求まる。

## 計算量

エラトステネスの篩：O(MloglogM) (ただし、M=N^(1/3))
二分探索：O(logM)
よって、総計算量は、
O(MloglogM + PlogP) (ただし、PはM以下の素数の数)

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

int main()
{
    ll n;
    cin >> n;

    vector<int> hurui(1001001);
    for (int i = 2; i <= 1e6; i++) {
        if (hurui[i]) continue;
        for (int j = i * 2; j <= 1e6; j += i) {
            hurui[j]++;
        }
    }

    vector<int> pn;
    rng(i, 2, 1e6 + 1) {
        if (!hurui[i]) pn.push_back(i);
    }

    ll ans = 0;
    for (auto q : pn) {
        ll ok = 1, ng = q;
        while (ng - ok > 1) {
            ll p = (ok + ng) / 2;
            if (p <= n / ((ll)q * q * q) && p < q) ok = p;
            else ng = p;
        }

        int pos = upper_bound(all(pn), ok) - pn.begin();
        if (pos != pn.size()) ans += pos;
    }

    cout << ans << endl;

    return 0;
}
```
