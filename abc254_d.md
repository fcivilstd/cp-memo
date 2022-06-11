---
tags:
    - 整数論
    - 平方数
---

# ABC254-D

[問題](https://atcoder.jp/contests/abc254/tasks/abc254_d)

## 考察

平方数には、素因数が偶数個になるという性質がある。i \* jが平方数になるためには、iの偶数個にならない素因数をjで補うようなペアであればよい。また、iの偶数個にならない素因数は、√i以下の全ての平方数で割りつくして残ったものである。よって、i=1~Nに関して、残った奇数個の素因数の積をインデックスでまとめて管理して、後から場合の数を求めるために2乗し、それを合計すれば解を得ることができる。

## 計算量

平方数で割りつくす：O(√N)
よって、総計算量は
O(N√N)

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
    int n;
    cin >> n;

    vi cnt(n + 1);
    rng(i, 1, n + 1) {
        int x = i;
        for (int j = 2; j * j <= n; j++) {
            while (x % (j * j) == 0) {
                x /= j * j;
            }
        }
        cnt[x]++;
    }

    int ans = 0;
    rng(i, 1, n + 1) ans += cnt[i] * cnt[i];

    cout << ans << endl;

    return 0;
}
```
