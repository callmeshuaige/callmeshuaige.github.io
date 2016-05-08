---
layout: post
title:  "BestCoder Round #79 (div.2) 1002 Claris and XOR"
date:   2016-04-10 17:30:32
categories: other
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<h3>题意很简洁，给出两个区间[a,b],[c,d]且a,b,c,d均不超过\(10^{18}\)
一般求最大异或值得解法就是贪心，从高位往低位贪即可，字典树也是这个原理，只不过上者需要O(n)的预处理，这题关键还是要知道若到了某一位两个数0,1均能取，那么后面肯定全为1。这样只要扫一遍就可以了。</h3>

{% highlight c++ %}
#include <iostream>
#include <cstdio>
#include <map>
#include <queue>
#include <vector>
#include <climits>
#include <cstring>
#include <cmath>
#include <algorithm>

#define LL long long

using namespace std;

LL a, b, c, d;

bool judge(LL l, LL r, LL n, LL m)
{
    if(l < n)
    {
        if(r >= n)return true;
    }
    if(l >= n && l <= m)return true;
    return false;
}

int main()
{
    int T;
    scanf("%d", &T);
    while(T--)
    {
        scanf("%I64d%I64d%I64d%I64d", &a, &b, &c, &d);
        LL l, r, left , right, ans;
        l = r = 0LL;
        bool la, lb, ra, rb;
        bool flag = false;
        for(LL i = 60LL; i >= 0LL; --i)
        {
            ra = rb = la = lb = false;
            left = l;
            right = l + (1LL << i) - 1LL;
            if(judge(left, right, a, b))la = true;
            left = l + (1LL << i);
            right = l + (1LL << (i + 1LL)) - 1LL;
            if(judge(left, right, a, b))lb = true;
            left = r;
            right = r + (1LL << i) - 1LL;
            if(judge(left, right, c, d))ra = true;
            left = r + (1LL << i);
            right = r + (1LL << (i + 1LL)) - 1LL;
            if(judge(left, right, c, d))rb = true;
            if(ra && rb && la && lb)
            {
                ans = (l ^ r) + (1LL << (i + 1LL)) - 1LL;
                flag = true;
                break;
            }
            if(ra && lb)
            {
                l = l + (1LL << i);
                continue;
            }
            if(rb && la)
            {
                r = r + (1LL << i);
                continue;
            }
            if(ra && la)
            {
                continue;
            }
            if(rb && lb)
            {
                l = l + (1LL << i);
                r = r + (1LL << i);
            }
        }
        if(!flag) ans = l ^ r;
        cout << ans << endl;
    }
    return 0;
}
{% endhighlight %}
