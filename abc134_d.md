---
tags:
    - 調和級数
---

# ABC134-D

[問題](https://atcoder.jp/contests/abc134/tasks/abc134_d)

## 考察

現時点でiの倍数の箱に含まれるボールの個数を数えることを考える。
必要なループ回数は、
N/1 + N/2 + N/3 + ... + N/N
となり、これは
N \* 調和級数
である。調和級数は、logNで上から押さえられるため、計算量は十分に小さい。

また、iの倍数はi以上であるから、i = 1から探索するよりもi = Nから探索するほうが都合が良い。

## 計算量

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
    int n;
    cin >> n;

    vi a(n);
    rep(i, n) cin >> a[i];

    int m = 0;
    vi cnt(n + 1);
    rrng(i, 1, n + 1) {
        int sum = 0;
        for (int j = 2 * i; j <= n; j += i) sum += cnt[j - 1];
        if (a[i - 1] != (sum & 1)) {
            cnt[i - 1] = 1;
            m++;
        }
    }

    vi ans;
    rep(i, n) if (cnt[i]) ans.push_back(i + 1);

    cout << m << endl;
    rep(i, ans.size()) cout << ans[i] << " \n"[i == ans.size() - 1];

    return 0;
}
```
