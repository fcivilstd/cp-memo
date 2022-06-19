---
tags:
    - LCS
    - 動的計画法
---

# AOJ- Longest Common Subsequence

[問題](https://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_10_C)

## 考察

## 計算量

O(|S||T|)

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

int solve(string& s, string& t)
{
    vvi dp(s.size() + 1, vi(t.size() + 1));
    rep(i, s.size()) rep(j, t.size()) {
        if (s[i] == t[j]) dp[i + 1][j + 1] = dp[i][j] + 1;
        else dp[i + 1][j + 1] = max(dp[i][j + 1], dp[i + 1][j]);
    }
    return dp[s.size()][t.size()];
}

int main()
{
    int q;
    cin >> q;

    rep(i, q) {
        string s, t;
        cin >> s >> t;
        cout << solve(s, t) << endl;
    }

    return 0;
}
```
