---
layout: post
title:  "Codeforces  Educational Codeforces Round 7 - F. The Sum of the k-th Powers"
date:   2016-02-17 12:18:32
categories: other
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<h3>题意很简明就是求 \(S_d(n) = \sum_{i=1}^{n}i^k\), 我们可以证明\(S_d(n)\)是关于 n 的 k+1 次的多项式，<a href="http://wenku.baidu.com/link?url=2QPccmUgeYDDfZ3l5lrGJLyrgBjrBSdFnRlI-o87A7GcZE6x0f-XNStMF2P-QeJL8mMYjC3nxM9iKwt_zVKRW1GAJM1rANxoDw48EAZwyxq">具体证明参考这里</a>
那么我们知道根据拉格朗日插值法,x 互不相同的 n+1 个点可以确定次数不超过 n 的多项式，那么这里我们需要 k+2 个点来确定这个 k+1 次的多项式，然后直接带入 n 的值即可求出 \(S_d(n)\)</h3>

```c++
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <vector>
#include <cstring>
#include <queue>
#include <climits>
#include <cmath>
#include <map>
#include <set>

#define LL long long

#define pr pair < int, int >

using namespace std;

LL MOD=1000000007;

LL fac[1100000],inv[1100000],p[1100000];

LL pow_mod(LL a,LL b,LL m){
    LL ans=1LL;
    a%=m;
    while(b){
        if(b&1)ans=ans*a%m;
        a=a*a%m;
        b>>=1;
    }
    return ans;
}

int main()
{
    fac[0]=1LL;
    for(LL i=1;i<=1010000;++i){
        fac[i]=i*fac[i-1]%MOD;
    }
    inv[1010000]=pow_mod(fac[1010000],MOD-2,MOD);
    for(LL i=1010000-1;i>=0;--i){
        inv[i]=inv[i+1]*(i+1)%MOD;
    }
    LL n,k;
    cin>>n>>k;
    for(LL i=1;i<=k+2;++i){
        p[i]=p[i-1]+pow_mod(i,k,MOD);
        p[i]%=MOD;
    }
    if(n<=k+2){
        cout<<p[n]<<endl;
        return 0;
    }
    LL x=1LL;
    for(LL i=1;i<=k+2;++i){
        x*=(n-i);
        x%=MOD;
    }
    LL ans=0LL,flag;
    for(LL i=1;i<=k+2;++i){
        if((k+2-i)&1)flag=-1;
        else flag=1;
        ans+=x*flag*pow_mod(n-i,MOD-2,MOD)%MOD*inv[i-1]%MOD*inv[k+2-i]%MOD*p[i];
        (ans+=MOD)%=MOD;
    }
    cout<<ans<<endl;
    return 0;
}
```