---
tags:
    - 最大公約数
    - 整数論
---

# ABC136-E

[問題](https://atcoder.jp/contests/abc136/tasks/abc136_e)

## 考察

ある数xを決め打ちしたとして、整数列をxの倍数にするためには、
各整数をxで割った余りに変換し、0にならない分を操作によって0にすればよい。

(最大)公約数の重要な性質として、
gcd(a, b, c, ...) = G としたとき、
(a + b + c + ...) % G = 0
となる。

また、操作の性質として、整数列の総和は操作の前後で変化しない。

つまり、ある数xの候補として整数列の総和の約数が挙げられる。
約数の数は総和の平方根に比例するため、全探索が可能な数に抑えられる。

## 計算量

約数全列挙：O(√(max(Ai)N))
条件の判定：O(NlogN)
よって、総計算量は
O(√(max(Ai)N) + NlogN)

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

int main()
{
    int n, k;
    cin >> n >> k;

    vi a(n);
    rep(i, n) cin >> a[i];

    int tot = 0;
    rep(i, n) tot += a[i];

    vi ds;
    for (int i = 1; i * i <= tot; i++) {
        if (tot % i == 0) {
            ds.push_back(i);
            if (i * i != tot) ds.push_back(tot / i);
        }
    }

    int ans = 0;
    for (auto x : ds) {
        int ptot = 0;
        vi ma;
        rep(i, n) {
            ma.push_back(a[i] % x);
            ptot += x - ma.back();
        }
        sort(all(ma));

        bool flag = false;
        int mtot = 0;
        rep(i, n) {
            mtot += ma[i];
            ptot -= x - ma[i];
            if (mtot == ptot) {
                if (max(mtot, ptot) <= k) {
                    flag = true;
                }
            }
        }

        if (flag) chmax(ans, x);
    }

    cout << ans << endl;

    return 0;
}
```
