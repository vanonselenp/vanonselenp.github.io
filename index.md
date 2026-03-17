---
layout: default
description: Peter van Onselen - Staff Engineer specializing in backend engineering, AWS cloud infrastructure, and technical leadership. 14+ years building scalable systems at The Economist.
---

{% if site.posts.size > 0 %}
{% assign latest_post = site.posts.first %}
<article class="post">
    <header class="post-header">
        <h1><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h1>
        <p class="post-meta">
            <time datetime="{{ latest_post.date | date_to_xmlschema }}">{{ latest_post.date | date: "%B %d, %Y" }}</time>
            {% if latest_post.categories.size > 0 %}
            in
            {% for category in latest_post.categories %}
                <span class="category">{{ category }}</span>{% unless forloop.last %}, {% endunless %}
            {% endfor %}
            {% endif %}
        </p>
    </header>

    <div class="post-content">
        {{ latest_post.content }}
    </div>

    <footer class="post-footer">
        <p><a href="{{ '/blog/' | relative_url }}">&larr; All posts</a></p>
    </footer>
</article>

{% else %}
<p>No posts yet. Check back soon!</p>
{% endif %}

---

## Quick Links

- [About Me](/about/) - Professional background and experience
- [Projects](/projects/) - Recent projects and technical contributions  
- [Contact](/contact/) - Get in touch for opportunities or discussions

---

*This site is built with Jekyll and hosted on GitHub Pages. Feel free to check out the [source code](https://github.com/vanonselenp/vanonselenp.github.io) if you're interested in the technical implementation.*
