---
tags:
    - 円環
    - 尺取り法
---

# 典型90-076

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bx)

## 考察

円環を直列化すると、境界を考慮することができない。しかし、円環を2周分直列化することで境界を考慮することができる。全体の大きさの10分の1となる連続するピースを選ぶには、尺取り法を使用すればよい。

## 計算量

尺取り法：O(N)
よって、総計算量は
O(N)

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

    ll tot = 0;
    vector<int> a(n), b;
    rep(i, n) {
        cin >> a[i];
        tot += a[i];
    }

    rep(i, n) b.push_back(a[i]);
    rep(i, n) b.push_back(a[i]);

    if (tot % 10) {
        cout << "No" << endl;
        return 0;
    }

    ll tb = 0;
    queue<int> q;
    rep(i, 2 * n) {
        q.push(b[i]);
        tb += b[i];

        while (tb > tot / 10) {
            int t = q.front(); q.pop();
            tb -= t;
        }

        if (tb == tot / 10) {
            cout << "Yes" << endl;
            return 0;
        }
    }

    cout << "No" << endl;

    return 0;
}
```
