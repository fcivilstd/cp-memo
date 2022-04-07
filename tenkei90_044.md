---
tags:
    - クエリ
---

# 典型90-044

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ar)

## 考察

愚直に配列の中身をずらすと、計算量はO(QN)となり、この問題の制約では厳しい。
しかし、実際に中身をずらさなくても、左端がどこに対応しているかだけ記録しておけば解を得ることができる。

## 計算量

swap：O(1)
左端の記録：O(1)
クエリの受け取り：O(Q)
よって、総計算量は
O(Q)

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
    int n, q;
    cin >> n >> q;

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    int s = 0;
    rep(i, q) {
        int t, x, y;
        cin >> t >> x >> y;
        x--; y--;

        if (t == 1) {
            swap(a[(n - s + x) % n], a[(n - s + y) % n]);
        } else if (t == 2) {
            s = (s + 1) % n;
        } else {
            cout << a[(n - s + x) % n] << endl;
        }
    }

    return 0;
}
```
