---
layout: page
title: Blog
permalink: /blog/
description: Technical blog by Peter van Onselen covering software engineering, cloud infrastructure, technical leadership, TDD practices, and game development insights.
---

{% assign latest_post = site.posts | first %}
<h3><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h3>
<p class="post-meta">{{ latest_post.date | date: "%B %d, %Y" }}
{% if latest_post.categories.size > 0 %}
•
{% for category in latest_post.categories %}
  <span class="category">{{ category }}</span>{% unless forloop.last %}, {% endunless %}
{% endfor %}
{% endif %}
</p>
{{ latest_post.content }}

---

## Previous Posts

{% for post in site.posts offset:1 %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

## Subscribe & Stay Updated

- **RSS Feed:** [Subscribe to updates]({{ "/feed.xml" | relative_url }})
- **LinkedIn:** [Follow me for professional updates](https://linkedin.com/in/peter-van-onselen-a46b1b2b)
- **GitHub:** [See my latest code and projects](https://github.com/vanonselenp)

## Suggest a Topic

Have a topic you'd like me to write about? Questions about technology, development practices, or career advice? I'd love to hear from you! [Send me a message](/contact/) with your suggestions or questions.

---

*Thank you for reading! I hope you find these insights helpful in your own professional journey.*
