---
layout: post
title:  "新的博客终于完工啦~"
date:   2016-05-02 21:50:32
categories: other
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
贴个sunday算法的模板
$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$
{% highlight c++ %}
int sunday(string s, string d)
{
    int lens = s.length();
    int lend = d.length();
    int next[26] = {0};
    for (int j = 0; j < 26; ++j)
        next[j] = lend + 1;
    for (int j = 0; j < lend; ++j)
        next[d[j] - 'a'] = lend - j;
    int pos = 0;
    while(pos < (lens - lend + 1))
    {
        int i = pos, j = 0;
        for(; j < lend; ++j, ++i)
        {
            if(s[i] == d[j])continue;
            pos += next[s[pos + lend] - 'a'];
            break;
        }
        if(j == lend)return pos + 1;
    }
    return -1;
}
{% endhighlight %}
