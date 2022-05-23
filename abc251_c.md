---
tags:
    - 比較関数
---

# ABC251-C

[問題](https://atcoder.jp/contests/abc251/tasks/abc251_c)

## 考察

オリジナルの内、一番得点が高く、一番順番が小さいものが求まるようにソートすればよい。

## 計算量

ソート：O(NlogN)

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

bool comp(const pair<int, int>& p1, const pair<int, int>& p2)
{
    if (p1.first != p2.first) return p1.first < p2.first;
    return p1.second > p2.second;
}

int main()
{
    int n;
    cin >> n;

    map<string, vector<pair<int, int>>> mp;
    rep(i, n) {
        string s;
        int t;
        cin >> s >> t;

        mp[s].push_back({t, i + 1});
    }

    vector<pair<int, int>> a;
    for (auto [s, v] : mp) {
        a.push_back(v.front());
    }

    sort(rall(a), comp);

    cout << a.front().second << endl;

    return 0;
}
```
