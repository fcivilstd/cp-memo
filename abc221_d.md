---
tags:
    - 座標圧縮
    - imos法
---

# ABC221-D

[問題](https://atcoder.jp/contests/abc221/tasks/abc221_d)

## 考察

ある区間に対して加算するクエリが大量にあるとき、imos法を使用すると高速にしょりすることができる。この問題では、そのままimos法を適用すると配列が大きくなりすぎるため、座標圧縮をする必要がある。その際、どこかで元々の区間の大きさを記憶しておく。また、座標圧縮をせず、mapを使用したimos法もできる。

## 計算量

座標圧縮：O(NlogN)
imos法：O(N)
よって総計算量は
O(NlogN)

## コーディング

座標圧縮 + imos法

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

    vi ab, a(n), b(n);
    rep(i, n) {
        cin >> a[i] >> b[i];
        ab.push_back(a[i]);
        ab.push_back(a[i] + b[i]);
    }

    sort(ab.begin(), ab.end());
    ab.erase(unique(ab.begin(), ab.end()), ab.end());

    map<int, int> mp1, mp2;
    rep(i, ab.size()) {
        int pos = lower_bound(ab.begin(), ab.end(), ab[i]) - ab.begin();
        mp1[pos] = ab[i];
        mp2[ab[i]] = pos;
    }
    
    vll ans(n + 1);
    vi imos(ab.size());
    rep(i, n) {
        imos[mp2[a[i]]]++;
        imos[mp2[a[i] + b[i]]]--;
    }
    rep(i, ab.size() - 1) imos[i + 1] += imos[i];
    rep(i, ab.size() - 1) ans[imos[i]] += mp1[i + 1] - mp1[i];

    rng(i, 1, n + 1) cout << ans[i] << " \n"[i == n];

    return 0;
}
```

map + imos法

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
 
    map<int, int> m;
    rep(i, n) {
        int a, b;
        cin >> a >> b;
        m[a]++; m[a + b]--;
    }
 
    int pre = 0, tot = 0;
    vector<int> ans(n + 1);
    for (auto [day, cnt] : m) {
        ans[tot] += day - pre;
        pre = day;
        tot += cnt;
    }
 
    rng(i, 1, n) cout << ans[i] << endl;
 
    return 0;
}
```
