---
layout: page
title: Incoherent Apothegm
---

-----

<!-- {% capture site_categories %}{% for category in site.categories %}{{ category | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %} -->
<!-- site_categories: {{ site_categories }} -->
<!-- {% assign category_words = site_categories | split:',' | sort %} -->
<!-- category_words: {{ category_words }} -->

<!-- {% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %} -->
<!-- site_tags: {{ site_tags }} -->
<!-- {% assign tag_words = site_tags | split:',' | sort %} -->
<!-- tag_words: {{ tag_words }} -->

<!-- &raquo; -->
<!-- date: "%B %d, %Y" -->
<!-- date: '%Y-%m-%d' -->

<div id="tags">
  <h1>By Category</h1>
  <ul class="tags">
  {% for item in (0..site.categories.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ category_words[item] | strip_newlines }}{% endcapture %}
    <li ><a href="#{{ this_word | cgi_escape }}" class="tag">{{ this_word }} <span>({{ site.categories[this_word].size }})</span></a></li>  
  {% endunless %}{% endfor %}
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
    <li ><a href="#{{ this_word | cgi_escape }}" class="tag">{{ this_word }} <span>({{ site.tags[this_word].size }})</span></a></li>
  {% endunless %}{% endfor %}
  </ul>

  {% for cat in (0..site.categories.size) %}{% unless forloop.last %}
    {% capture this_category %}{{ category_words[cat] | strip_newlines }}{% endcapture %}
    <h2 id="{{ this_category | cgi_escape }}">{{ this_category | upcase }}</h2>
    {% for item in (0..site.tags.size) %}{% unless forloop.last %}
      {% capture this_tag %}{{ tag_words[item] | where: "category", this_category | strip_newlines }}{% endcapture %}
    <h2 id="{{ this_tag | cgi_escape }}">{{ this_tag }}</h2>
    <ul class="posts">
      {% for post in site.tags[this_tag] %}{% if post.title != null %}
      <li itemscope><span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date_to_string }}</time></span> <a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endif %}{% endfor %}
    </ul>
    {% endunless %}{% endfor %}
  {% endunless %}{% endfor %}
</div>

# By Date
<div id="dates">
  <ul class="posts">
  {% for post in site.posts %}
    <li itemscope><span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date_to_string }}</time></span> <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
</div>