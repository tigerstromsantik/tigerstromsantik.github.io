---
layout: default
---
<h2 class="category">Hantera</h2>

<h3 class="period">Objekt</h3>
<br/>
{% capture posts %}
  {% for post in site.posts %}
    |{{ post.item.ref }}#{{ post.title }}#{{ post.item.price }}#{{ post.sold }}#{{ post.path }}
  {% endfor %}
{% endcapture %}
{% assign sortedposts = posts | split: '|' | sort %}
<table class="vlines">
<tr>
  <th>Ref</th><th>Title</th><th>Price</th><th>Sold</td><th>Path</th>
</tr>
{% for post in sortedposts %}
  {% assign field = post | split: '#' %}
  {% unless field[4] == empty %}
<tr>
  <td><b>{{field[0]}}</b></td>
  <td>{{field[1]}}</td>
  <td>{{field[2]}}</td>
  <td>{% if field[3] == 'true' %}<span class="sold">såld</span>{% endif %}</td>
  <td><a href='https://github.com/tigerstromsantik/tigerstromsantik.github.io/edit/master/{{field[4]}}'><code>{{field[4]}}</code></a></td>
</tr>
{% endunless %}
{% endfor %}
</table>
