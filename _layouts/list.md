---
layout: default
---

<h2 class="category">{{page.title}}</h2>

{{ content }} 

<br/>
{% for period in page.periods %}
{% unless period == "*" %}
<h3 class="period">{% if period != "?" %}{{period}}{% else %}okänt{% endif %}</h3>
{% endunless %}

{% assign limit = page.limit %}
<table class="list">
{% for post in site.posts %}
 {% capture posttime %}{{post.date | plus: monthmillis }}{% endcapture %}
 {% if (page.category == empty or page.category contains post.item.kind) and (period == "*" or post.item.decade == period or (period == "?" and post.item.decade == null )) %}
  {% if page.sold == post.sold or (page.sold == false and post.sold == null) %}
   {% if page.limit == null or limit > 0 %}
    {% assign limit = limit | minus: 1 %}
	<tr>
    <td colspan="2" class="spacer"></td>
	</tr>
  <tr>
    <td valign="top" width="300" class="img" rowspan="2">
      <a href="{{ post.url }}"><img src="{{ post.item.image | replace_first: '/upload/', '/upload/w_300,h_300,c_fit/' }}" alt="{{ post.title }}" /></a>
    </td>
    <td valign="top">
      <span class="date">{{ post.date | date_to_string }}</span>
      <h4>{{ post.title }}</h4>
      {% if post.item.desc %}<div class="desc">{{ post.item.desc }}</div>{% endif %}
	    <span class="price">
      {% if post.sold %}
      <span class="sold">såld</span>
      {% else %}
	     {% if post.item.price %}{{ post.item.price }} <small>SEK</small>{% endif %}
      {% endif %}
			</span>
		</td>
  </tr>
	<tr valign="bottom">
    <td class="listtext">
      {{ post.content | truncatewords: 40, '...' }}
		</td>
	</tr>
   {% endif %}
  {% endif %}
 {% endif %}
{% endfor %}
</table>
{% endfor %}

