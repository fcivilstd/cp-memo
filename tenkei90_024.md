---
tags:
    - 偶奇性
---

# 典型90-024

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_x)

## 考察

"Yes"となる条件は、

- 操作の最小回数がK以下であること
- AとBが一致した後に一か所ずらして元に戻すために追加で2回操作が必要であるため、偶奇が一致していること

の二つである。

## 計算量

操作の最小回数を数える：O(N)
偶奇の一致を判定する：O(1)
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
    int n, k;
    cin >> n >> k;

    vector<int> a(n), b(n);
    rep(i, n) cin >> a[i];
    rep(i, n) cin >> b[i];

    ll diff = 0;
    rep(i, n) diff += abs(a[i] - b[i]);

    if (diff <= k && (diff & 1) == (k & 1)) cout << "Yes" << endl;
    else cout << "No" << endl;

    return 0;
}
```
