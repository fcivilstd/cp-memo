---
tags:
    - 二分探索
---
# 典型90-001

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_a)

## 考察

スコアの最小値は1、最大値はLである。
正解のスコアを得られた場合、そのスコア以下のスコアは達成でき、そのスコアを超えるスコアは達成できない。
これらのことから、二分探索で正解のスコアを決め打ちすれば良いことに気づける。

決め打ちしたスコア(X)が達成可能性を判定する必要がある。
判定するためには、N個の切れ目を左端から見ていき、X以上の塊を作ることができた場合にその切れ目を採用する。
K個の切れ目を採用するまでこれを続ける。

## 計算量

スコアを決め打ちする二分探索：O(logL)
決め打ちしたスコアを達成できるかの判定：O(N)
よって、総計算量は
O(NlogL)

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
    int n, l, k;
    cin >> n >> l >> k;

    vector<int> a(n + 1);
    rep(i, n) cin >> a[i];
    a[n] = l;

    int ok = 0, ng = 1 << 30;
    auto f = [&](int x) {
        if ((ll)x * (k + 1) > l) return false;
        int tmp = 0, cnt = 0;
        rep(i, n + 1) {
            if (cnt < k && a[i] - tmp >= x) {
                tmp = a[i];
                cnt++;
            }
            if (i == n) {
                if (a[i] - tmp >= x) return true;
                else return false;
            }
        }
    };

    while (ng - ok > 1) {
        int mid = (ok + ng) / 2;
        if (f(mid)) ok = mid;
        else ng = mid;
    }

    cout << ok << endl;

    return 0;
}
```
