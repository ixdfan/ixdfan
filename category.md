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
<h2><a name="{{ category | first }}">{{ category | first }}</a><span style="margin-left:30px;font-weight:normal;font-size:24px;">{{ category | last | size }}</span></h2>

<ul class="arc-list" style="padding:0;">
    {% for post in category.last %}
        <li style="list-style-type:none;border-bottom:1px solid #ccc;line-height:45px"><a href="{{ post.url }}" style="border:none;">{{ post.title }}</a><span style="float:right">{{ post.date | date:"%d/%m/%Y"}}</span></li>
    {% endfor %}
</ul>
{% endfor %}
<div class="post-category" style="position:fixed;left:50px;top:250px;font-size:12px;">
  <h4>Category</h4>
  	<ul>
  		    
  	 {% for category in site.categories %}
      		<li><a href="http://ixdfan.github.com/Category/#{{ category | first }}" title="view all
  			posts">{{ category | first }} {{ category | last | size }}</a>
      		</li>
  	{% endfor %}
  	</ul>
	</div>
