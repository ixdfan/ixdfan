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

<ul class="arc-list">
    {% for post in category.last %}
        <li style="width:700px"><a href="{{ post.url }}" >{{ post.title }}<span style="float:right">{{ post.date | date:"%d/%m/%Y"}}</span></a></li>
    {% endfor %}
</ul>
{% endfor %}