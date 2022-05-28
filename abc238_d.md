---
tags:
    - bit演算
    - 論理積
    - 排他的論理和
---

# ABC238-D

[問題](https://atcoder.jp/contests/abc238/tasks/abc238_d)

## 考察

x + y = (x xor y) + (x and y) * 2;
_____               _________
  ↓                     ↓
  s                     a

(x xor y) and (x and y)が0になるとき、この分解が可能になる。
これは、xとyを二進表記したとき、(x and y)で1になる位の集合Aと(x xor y)で0になる位の集合Bの積集合A∩Bは空集合となるためである。

## 計算量

クエリの受け取り：O(T)
判定：O(1)
よって、総計算量は
O(T)

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
    int t;
    cin >> t;

    while (t--) {
        ll a, s;
        cin >> a >> s;

        if (2 * a <= s && ((s - 2 * a) & a) == 0) {
            cout << "Yes" << endl;
        } else {
            cout << "No" << endl;
        }
    }

    return 0;
}
```
