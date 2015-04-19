---
layout: page
title: "分类目录"
date: 2015-04-10 23:11
comments: true
sharing: false
footer: true
---

<style type="text/css">
    li {
        float:left;
        margin-right:20px;
        margin-top:20px;
        list-style-type:none;
    }

</style>

<ul>
{% for item in site.categories %}
    <li><a href="/blog/categories/{{ item[0] }}/">{{ item[0] | capitalize }}</a> [ {{ item[1].size }} ]</li>
{% endfor %}
</ul>
