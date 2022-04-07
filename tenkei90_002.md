---
tags:
    - 全探索
    - bit全探索
---

# 典型90-002

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_b)

## 考察

制約がN<=20と小さいことから全探索が可能であると気づける。
カッコの種類は"("と")"の2種類であるため、bit全探索が可能である。

候補であるカッコ列が正しいカッコ列であるかの判定は、

- "("で1加算、")"で1減算した場合に合計値がどこで中断しても0以上であること
- 上記の最終的な合計値が0であること

の2つを満たしていかで可能である。

## 計算量

bit全探索：O(2^N)
正しいカッコ列であるかの判定：O(N)
よって、総計算量は
O(N*2^N)

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

string conv(int x, int n)
{
    string ret = "";
    for (int i = n - 1; i >= 0; i--) {
        if (x & (1 << i)) {
            // )
            ret += ")";
        } else {
            // (
            ret += "(";
        }
    }
    return ret;
}

int main()
{
    int n;
    cin >> n;

    for (int bit = 0; bit < 1 << n; bit++) {
        int cnt = 0;
        bool flag = true;
        for (int i = n - 1; i >= 0; i--) {
            if (bit & (1 << i)) {
                // )
                cnt--;
            } else {
                // (
                cnt++;
            }
            if (cnt < 0) flag = false;
        }
        if (cnt == 0 && flag) cout << conv(bit, n) << endl;
    }

    return 0;
}
```
