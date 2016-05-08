---
layout: post
title:  "HDU 5592 ZYB's Premutation"
date:   2016-02-17 12:18:32
categories: other
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<h3>好久没有更新博客了--<br/>
早上洗澡的时候忽然想起来很久前BC没有AC的一题，题意比较简单，很容易转化为给出一个序列每个元素的逆序数，要求原序列的值。<br/>

思路就是从后往前求，这样对于每个值就是当前在序列中的第K大，那么用树状数组+类似lower_bound的二分，就可以求出这个值，再把那个值更新为0就是-1，OK了==</h3>

```c++
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
#include <vector>
#include <map>
#include <climits>
#include <algorithm>

#define LL long long

using namespace std;

int a[50005],b[50005],c[4*50005],d[50005],n;

int lowbit(int x){return (x)&(-x);}

void update(int x,int d){
    while(x<=n){
        c[x]+=d;
        x+=lowbit(x);
    }
}

int sum(int x){
    int ans=0;
    while(x>=1){
        ans+=c[x];
        x-=lowbit(x);
    }
    return ans;
}

vector <int> v;

int main()
{
    int T;scanf("%d",&T);
    while(T--){
        v.clear();
        memset(c,0,sizeof(c));
        scanf("%d",&n);
        for(int i=0;i<n;++i){
            scanf("%d",a+i);
        }
        for(int i=1;i<n;++i)d[i]=a[i]-a[i-1];
        for(int i=0;i<n;++i)b[i]=i-d[i]+1,update(i+1,1);
        int l,r,mid;
        for(int i=n-1;i>=0;--i){
            l=1;r=n;mid=(l+r)>>1;
            while(l<r){
                if(sum(mid)<b[i])l=mid+1;
                else r=mid;
                mid=(l+r)>>1;
            }
            v.push_back(mid);
            update(mid,-1);
        }
        reverse(v.begin(),v.end());
        int len=(int)v.size();
        for(int i=0;i<len;++i){
            if(i)putchar(' ');
            printf("%d",v[i]);
        }
        puts("");
    }
    return 0;
}

```