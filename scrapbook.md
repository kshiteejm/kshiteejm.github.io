---
layout: page
title: Incoherent Apothegm
---

-----

<div id="tags">
  <h1>By Category</h1>
  <table class="category-table">
  {% for category in site.categories %}
    {% capture this_category %}{{ category[0] | strip_newlines }}{% endcapture %}
    
    <tr>
    <th class="left-width-dynamic">
    <a href="#{{ this_category | cgi_escape }}" class="category">{{ this_category }} <span>({{ site.categories[this_category].size }})</span></a>
    </th>
    <th class="right-width-dynamic">
    <ul class="tags">
    {% assign sorted_tags = site.tags | sort %}
    {% for tag in sorted_tags %}
      {% assign this_tag = tag[1] | where: "category", this_category %}
      {% if this_tag != empty %}
      <li ><a href="#{{ tag[0] | cgi_escape }}" class="tag">{{ tag[0] }} <span>({{ this_tag.size }})</span></a></li>
      {% endif %}
    {% endfor %}
    </ul>
    </th>
    </tr>
  {% endfor %}
  </table>

  {% for category in site.categories %}
    {% capture this_category %}{{ category[0] | strip_newlines }}{% endcapture %}
    <h2 id="{{ this_category | cgi_escape }}">{{ this_category | upcase }}</h2>
    {% assign sorted_tags = site.tags | sort %}
    {% for tag in sorted_tags %}
      {% assign this_tag = tag[1] | where: "category", this_category %}
      {% if this_tag != empty %}
      <h2 id="{{ tag[0] | cgi_escape }}">{{ tag[0] }}</h2>
      <ul class="posts">
        {% for post in this_tag %}{% if post.title != null %}
          <li itemscope><span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date_to_string }}</time></span> <a href="{{ post.url }}">{{ post.title }}</a></li>
        {% endif %}{% endfor %}
      </ul>
      {% endif %}
    {% endfor %}
  {% endfor %}
</div>

# By Date
<div id="dates">
  <ul class="posts">
  {% for post in site.posts %}
    <li itemscope><span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date_to_string }}</time></span> <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
</div>