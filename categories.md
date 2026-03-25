---
layout: default
title: 文章分类
permalink: /categories/
---

# 📂 文章分类

{% assign categories = site.posts | map: "categories" | uniq %}
{% for category in categories %}
{% if category and category != "" %}
<div class="category-section">
  <h2 id="{{ category | slugify }}">📁 {{ category }}</h2>
  <ul class="post-list">
    {% for post in site.posts %}
      {% if post.categories contains category %}
      <li>
        <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
        <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 15 }}</p>
        {% if post.tags %}
        <div class="post-tags">
          {% for tag in post.tags %}
          <span class="tag">#{{ tag }}</span>
          {% endfor %}
        </div>
        {% endif %}
      </li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
{% endif %}
{% endfor %}
