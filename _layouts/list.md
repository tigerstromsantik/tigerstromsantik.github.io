---
layout: default
---

<h2 class="category">{{page.title}}</h2>

{{ content }} 

<br/>
{% for period in page.periods %}
<h3 class="period">{% if period != "?" %}{{period}}{% else %}okänt{% endif %}</h3>

<table class="list">
{% for post in site.posts %}
 {% if page.category == empty or (page.category contains post.item.kind and (post.item.decade == period or (period == "?" and post.item.decade == null ))) %}
  {% if page.sold == post.sold or (page.sold == false and post.sold == null) %}
  <tr>
    <td valign="top" width="300" class="img" rowspan="2">
      <a href="{{ post.url }}"><img src="{{ post.item.image | replace_first: '/upload/', '/upload/w_300,h_300,c_fit/' }}" alt="{{ post.title }}" /></a>
    </td>
    <td valign="top">
      <h4>{{ post.title }}</h4>
			<span class="price">
      {% if post.sold %}
      <span class="sold">såld</span>
      {% else %}
	     {% if post.item.price %}{{ post.item.price }} SEK{% endif %}
      {% endif %}
			</span>
		</td>
  </tr>
	<tr valign="bottom">
    <td class="listtext">
      {{ post.content | truncatewords: 30, '...' }}
		</td>
	</tr>
  {% endif %}
 {% endif %}
{% endfor %}
</table>
{% endfor %}

