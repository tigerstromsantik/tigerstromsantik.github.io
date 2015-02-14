---
layout: default
---

<h2 class="category">{{page.category | join: ' &amp; ' }}</h2>

{{ content }} 

<br/>
{% for period in page.periods %}
<h3 class="period">{% if period != "?" %}{{period}}{% else %}okänt{% endif %}</h3>

<table class="list">
{% for post in site.posts %}
 {% if page.category contains post.item.kind and (post.item.decade == period or (period == "?" and post.item.decade == null )) %}
  {% unless post.item.sold %}
  <tr>
    <td valign="top" width="350" class="img" rowspan="2">
      <a href="{{ post.url }}"><img src="{{ post.item.image | replace_first: '/upload/', '/upload/w_300,h_300,c_fit/' }}" alt="{{ post.title }}" /></a>
    </td>
    <td valign="top" width="300">
      <h4>{{ post.title }}</h4>
		</td>
  </tr>
	<tr valign="bottom">
		<td class="itemtext">
      {{ post.content }}
		</td>
	</tr>
  {% endunless %}
 {% endif %}
{% endfor %}
</table>
{% endfor %}

