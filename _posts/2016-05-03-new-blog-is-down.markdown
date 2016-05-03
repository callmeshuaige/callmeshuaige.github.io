---
layout: post
title:  "新的博客终于完工啦~"
date:   2016-05-02 21:50:32
categories: other
---

>贴个sunday算法的模板
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
