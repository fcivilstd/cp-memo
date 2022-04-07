---
tags:
    - 最小公倍数
    - 最大公約数
    - オーバーフロー
---

# 典型90-38

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_al)

## 考察

最大公約数と最小公倍数の関係は、

A \* B = GCD(A, B) \* LCM(A, B)

オーバーフローを回避するためには、次の式を使うと良い。
(int)A <= floor((float)B) - (※)
今回の問題では、式変形によって
B / GCD(A, B) <= floor(10^18 / A)
とすると、左辺は絶対に整数になるため式(※)を満足する。しかし、
A <= floor(GCD(A, B) / B \* 10^18)
としてしまうと、
誤差で正しい解が得られないため注意が必要である。

## 計算量

最大公約数の計算：O(log(min(A, B)))
最小公倍数が10^18を超えるかどうかの判定：O(1)
よって、総計算量は
O(log(min(A, B)))

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

const ll p18 = 1e18;

int main()
{
    ll a, b;
    cin >> a >> b;

    ll c = b / gcd(a, b);
    if (p18 / a >= c) cout << a * c << endl;
    else cout << "Large" << endl;

    return 0;
}
```
