---
layout: default
---

{% for post in site.posts %}

<article>
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date | date: "%b %-d, %Y"}} by {{ post.author}} </span>
  </p>
  <div class="content">
       {{ post.content | strip_html | truncate:200 }}
  </div>
</article>
{% endfor %}
