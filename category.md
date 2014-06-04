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
<h2>{{ category | first }}<span>{{ category | last | size }}</span></h2>

<ul class="arc-list">
    {% for post in category.last %}
        <li><a href="{{ post.url }}">{{ post.title }}</a>{{ post.date | date:"%d/%m/%Y"}}</li>
    {% endfor %}
</ul>
{% endfor %}