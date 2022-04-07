---
tags:
    - 貪欲法
---

# 典型90-048

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_av)

## 考察

1分で得られる得点は、i問目を解いて得られるBi点か、既に部分点を得ているj問目で満点を取って得られるAj - Bj点であると場合分けできる。後は、priority_queueにこれらの得点を全ていれ、1分を消費しながら貪欲に得点を上げていけば解が得られる。

## 計算量

priority_queueによるソート：O(NlogN)
K分間のシミュレーション：O(K)
よって、総計算量は
O(NlogN)

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

    priority_queue<int> q;
    rep(i, n) {
        ll a, b;
        cin >> a >> b;
        q.push(b);
        q.push(a - b);
    }

    ll ans = 0;
    while (k && q.size()) {
        int t = q.top(); q.pop();
        ans += t;
        k--;
    }
    
    cout << ans << endl;

    return 0;
}
```
