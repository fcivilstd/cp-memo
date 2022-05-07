---
tags:
    - 区間スケジューリング
---

# ABC103-D

[問題](https://atcoder.jp/contests/abc103/tasks/abc103_d)

## 考察

できるだけ少ない橋の本数で多くの要望に答えるためには、[a, b]の区間が重なっている位置の橋を取り除けば良い。つまり、重ならない区間の数が解となる。重ならない区間の数を求める問題は、区間スケジューリング問題に帰着できる。

## 計算量

区間の橋でソート：O(NlogN)
重ならない区間を数える：O(M)
よって、総計算量は
O(NlogN + M)

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
    int n, m;
    cin >> n >> m;

    vector<pair<int, int>> vi;
    rep(i, m) {
        int a, b;
        cin >> a >> b;

        vi.emplace_back(b, a);
    }

    sort(all(vi));

    int ans = 0;
    int preb = -1;
    for (auto [b, a] : vi) {
        if (preb <= a) {
            ans++;
            preb = b;
        }
    }

    cout << ans << endl;

    return 0;
}
```
