---
layout: page
permalink: /Category/
title: Category
modified: 2013-09-13
image:
  feature: so-simple-sample-image-4.jpg
  credit: Michael Rose
  creditlink: http://mademistakes.com
---
{% for category in site.categories %}
<h2>{{ category | first }}<span style="margin-left:30px;font-weight:normal">{{ category | last | size }}</span></h2>

<ul class="arc-list" style="padding:0;">
    {% for post in category.last %}
        <li style="list-style-type:none;border-bottom:1px solid #ccc;line-height:45px"><a href="{{ post.url }}" style="border:none;">{{ post.title }}</a><span style="float:right">{{ post.date | date:"%d/%m/%Y"}}</span></li>
    {% endfor %}
</ul>
{% endfor %}