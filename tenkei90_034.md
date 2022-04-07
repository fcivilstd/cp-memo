---
tags:
    - 尺取り法
---

# 典型90-034

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ah)

## 考察

愚直に考えると、連続する部分列を全探索してその中に含まれる整数の種類を数えることで解を得ることができるが、計算量がO(N^2)となり、この問題の制約では厳しい。
尺取り法を使えば連続する部分列の全探索を効率的に行うことができる。

## 計算量

尺取り法：O(N)
mapへの値の追加・削除(logN)
よって、総計算量は
O(NlogN)

## コーディング

queueを使用しない場合

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

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    int ans = 0;
    int r = -1;
    map<int, int> mp;
    for (int l = 0; l < n; l++) {
        while (r < n - 1) {
            if (!mp.count(a[r + 1]) && mp.size() >= k) break;
            r++;
            mp[a[r]]++;
        }

        chmax(ans, r - l + 1);

        mp[a[l]]--;
        if (mp[a[l]] == 0) mp.erase(a[l]);
    }

    cout << ans << endl;

    return 0;
}
```

queueを使用する場合

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

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    int ans = 0;
    map<int, int> mp;
    deque<int> q;

    rep(i, n) {
        q.push_back(a[i]);
        mp[a[i]]++;
        
        while (mp.size() > k) {
            int t = q.front(); q.pop_front();
            mp[t]--;
            if (mp[t] == 0) mp.erase(t);
        }

        chmax(ans, q.size());
    }

    cout << ans << endl;

    return 0;
}
```
