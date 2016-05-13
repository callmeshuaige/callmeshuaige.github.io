---
layout: post
title:  "Codeforces Round #352 (Div. 2) C. Recycling Bottles"
date:   2016-05-12 21:01:32
categories: other
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<h3>二维平面上，给出a,b两人的起始位置和回收桶的位置，接着给出n个垃圾的位置，问两人把垃圾都送回回收桶最短路程和是多少？<br/>
很容易想出无非三种情况：<br/>
<ul>
	<li>
		a一个人把所有垃圾收拾完
	</li>
	<li>	
		b一个人把所有垃圾收拾完
	</li>
	<li>
		a、b一起收拾
	</li>
</ul>
a、b只要都选中了起始去的位置后面距离就是固定的，然后排序完暴力枚举即可。
</h3>

{% highlight c++ %}
#include <iostream>
#include <cstdio>
#include <cstring>
#include <set>
#include <cmath>
#include <vector>
#include <algorithm>

using namespace std;

double eps = 1e-10;

double dcmp(double x)
{
    return (x > eps) - (x < -eps);
}

struct point
{
    double x,y;
}p[100005],a,b,t;

double dis(point a, point b)
{
    return sqrt((a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y));
}

struct r{
    double sum;
    int id;
}q;

vector <r> v;

bool cmp(r a,r b)
{
    return dcmp (a.sum - b.sum) == -1;
}

int main()
{
    cin >> a.x >> a.y;
    cin >> b.x >> b.y;
    cin >> t.x >> t.y;
    int n;
    cin >> n;
    for(int i = 0; i < n; ++i){
        scanf("%lf%lf", &p[i].x, &p[i].y);
    }
    double ans = 0.0;
    for(int i = 0; i < n; ++i){
        ans += 2.0 * dis(t, p[i]);
    }
    double res = 0.0, tmp;
    bool flag = true;
    for(int i = 0; i < n; ++i){
        tmp = dis(p[i], a) + ans - dis(t, p[i]);
        if(flag) {
            res = tmp;
            flag = false;
        }
        else {
            if(dcmp(tmp - res) == -1)res = tmp;
        }
        q.id = i;
        q.sum = dis(p[i], a) - dis(t, p[i]);
        v.push_back(q);
    }
    sort(v.begin(),v.end(),cmp);
    for(int i = 0; i < n; ++i){
        tmp = dis(p[i], b) + ans - dis(p[i], t);
        if(dcmp(tmp - res) == -1)res = tmp;
    }
    double w;
    for(int i = 0; i < n; ++i){
        tmp = dis(p[i], b) + ans - dis(p[i], t);
        for(int j = 0; j < n; ++j){
            if(v[j].id == i)continue;
            w = tmp + v[j].sum;
            if(dcmp(w - res) == -1)res = w;
            break;
        }
    }
    printf("%.10lf\n", res);
    return 0;
}

{% endhighlight %}
