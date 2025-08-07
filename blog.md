---
layout: page
title: A Blog of dubious intent
permalink: /blog/
---

Welcome to my blog! Here I share thoughts on technology, software development, leadership, and insights from my professional journey. Whether you're a fellow developer, a technology leader, or someone interested in the industry, I hope you find something valuable here.

## Recent Posts

{% for post in site.posts limit:5 %}
<div class="card">
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}
  {% if post.categories.size > 0 %}
  •
  {% for category in post.categories %}
    <span class="category">{{ category }}</span>{% unless forloop.last %}, {% endunless %}
  {% endfor %}
  {% endif %}
  </p>
  <p>{{ post.excerpt | strip_html | truncatewords:30 }}</p>
  <a href="{{ post.url | relative_url }}">Read more →</a>
</div>
{% endfor %}

## Post Archive

{% if site.posts.size > 5 %}
### All Posts
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
{% else %}
*Archive will appear here as more posts are published.*
{% endif %}

## Subscribe & Stay Updated

- **RSS Feed:** [Subscribe to updates]({{ "/feed.xml" | relative_url }})
- **LinkedIn:** [Follow me for professional updates](https://linkedin.com/in/peter-van-onselen-a46b1b2b)
- **GitHub:** [See my latest code and projects](https://github.com/vanonselenp)

## Suggest a Topic

Have a topic you'd like me to write about? Questions about technology, development practices, or career advice? I'd love to hear from you! [Send me a message](/contact/) with your suggestions or questions.

---

*Thank you for reading! I hope you find these insights helpful in your own professional journey.*
