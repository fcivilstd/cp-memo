---
tags:
    - 二分探索
---

# 典型90-007

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_g)

## 考察

愚直に考えると、各生徒ごとに最も近いクラスのレーティングを線形探索することで解を得ることができるが、計算量がO(QN)となり、この問題の制約では厳しい。
最も近いクラスのレーティングを探索すればよいので、ソートして二分探索するのが効率的であることに気づける。

## 計算量

ソート：O(NlogN)
二分探索：O(logN)
よって、総計算量は
O(NlogN + QlogN)
→O((N + Q)logN)

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
    int n;
    cin >> n;

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    int q;
    cin >> q;

    vector<int> b(q);
    rep(i, q) cin >> b[i];

    sort(all(a));

    rep(i, q) {
        int bi = b[i];
        auto itr = lower_bound(all(a), bi);

        int ans = 1 << 30;
        if (itr == a.begin()) {
            ans = abs(*itr - bi);
        } else if (itr == a.end()) {
            ans = abs(*prev(itr) - bi);
        } else {
            ans = abs(*itr - bi);
            chmin(ans, abs(*prev(itr) - bi));
        }

        cout << ans << endl;
    }

    return 0;
}
```
