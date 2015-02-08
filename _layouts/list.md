---
layout: default
---

{{ content }} 

<div id="list" class="{{ page.theme }}" style="padding: 10px; ">
<h2>{{page.category}}</h2>

{% assign counter = 0 %}
<table>
<tr>
{% for post in site.posts %}
{% if post.categories contains page.category %}
{% assign counter = counter | plus: 1 %}
{% assign cmod = counter | modulo:3 %}
<td>
{{ post.title }}<br/>
<a href="{{ post.url }}"><img src="{{ post.image }}" class="thumb" alt="{{ post.title }}" width="250" height="250" /></a>
</td>
{% if cmod == 0 %}
</tr>
<tr>
{% endif %}
{% endif %}
{% endfor %}

{% if cmod != 0 %}
<td></td>
{% assign counter = counter | plus: 1 %}
{% assign cmod = counter | modulo:3 %}
{% endif %}
{% if cmod != 0 %}
<td></td>
{% endif %}
</tr>
</table>
</div>
