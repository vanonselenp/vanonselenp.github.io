---
layout: default
description: Peter van Onselen - Staff Engineer specializing in backend engineering, AWS cloud infrastructure, and technical leadership. 14+ years building scalable systems at The Economist.
---

Hello! I'm **Peter van Onselen**, a technology professional based in **London, UK**. I specialize in software development, technical leadership, and building innovative solutions that drive business value.

With 14+ years of software development and team leadership, I'm passionate about creating scalable, efficient solutions and mentoring the next generation of developers. My expertise spans across backend engineering, cloud infrastructure, and developer experience.

**Current Focus:** Staff Engineer at the Economist  
**Specialties:** Backend Engineering, Cloud Infrastructure (AWS), Performance Optimization, API Architecture, Team Leadership & Mentoring

---

## Latest Blog Post

{% if site.posts.size > 0 %}
{% assign latest_post = site.posts.first %}
<div class="card">
  <h2><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h2>
  <p class="post-meta">{{ latest_post.date | date: "%B %d, %Y" }}
  {% if latest_post.categories.size > 0 %}
  •
  {% for category in latest_post.categories %}
    <span class="category">{{ category }}</span>{% unless forloop.last %}, {% endunless %}
  {% endfor %}
  {% endif %}
  </p>
  <div class="post-excerpt">
    {{ latest_post.excerpt }}
  </div>
  <a href="{{ latest_post.url | relative_url }}" class="btn">Read full post →</a>
</div>

{% if site.posts.size > 1 %}
{% assign next_post = site.posts[1] %}
<p><strong>Previous post:</strong> <a href="{{ next_post.url | relative_url }}">{{ next_post.title }}</a></p>
{% endif %}

<p><a href="/blog/">View all posts →</a></p>

{% else %}
<div class="card">
  <h2>Welcome to My Blog</h2>
  <p>I'm just getting started with this blog. Check back soon for posts on technology, software development, and lessons learned from my career.</p>
  <p>In the meantime, feel free to <a href="/about/">learn more about me</a> or <a href="/contact/">get in touch</a>.</p>
</div>
{% endif %}

---

## Quick Links

- [About Me](/about/) - Professional background and experience
- [Projects](/projects/) - Recent projects and technical contributions  
- [Contact](/contact/) - Get in touch for opportunities or discussions

---

*This site is built with Jekyll and hosted on GitHub Pages. Feel free to check out the [source code](https://github.com/vanonselenp/vanonselenp.github.io) if you're interested in the technical implementation.*
