---
layout: page
title: about me
tagline:
---
{% include JB/setup %}

<img src="assets/images/andrew.jpg" style="float: left;" />

<span style="width: 50%; float: left; margin-left: 50px;" >I'm a programmer with a .NET background currently learning python, and using it to learn more about algorithms, data science, machine learning, and general programming.
</span> <br style="clear: left;" >

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>