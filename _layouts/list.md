---
layout: default
---

{{ content }} 

<div id="list" class="{{ page.theme }}" style="padding: 10px; ">
<h2>{{page.category}}</h2>

{% assign counter = 0 %}
<table width="100%" cellspacing="0" cellpadding="4">
<tr>
{% for post in site.posts %}
{% if post.categories contains page.category %}
  {% unless post.sold %}
    {% assign counter = counter | plus: 1 %}
    {% assign cmod = counter | modulo:3 %}
<td valign="top">
<h4>{{ post.title }}</h4>
<a href="{{ post.url }}"><img src="{{ post.image | replace_first: '/upload/', '/upload/w_250,h_250,c_pad,f_png/' }}" class="thumb" alt="{{ post.title }}" width="250" /></a>
</td>
    {% if cmod == 0 %}
</tr>
<tr>
    {% endif %}
  {% endunless %}
{% endif %}
{% endfor %}

{% if cmod != 0 %}
<td width="33%"></td>
{% assign counter = counter | plus: 1 %}
{% assign cmod = counter | modulo:3 %}
{% endif %}
{% if cmod != 0 %}
<td width="33%"></td>
{% endif %}
</tr>
</table>
</div>
