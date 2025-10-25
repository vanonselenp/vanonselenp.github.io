---
layout: page
title: A Blog of dubious intent
permalink: /blog/
description: Technical blog by Peter van Onselen covering software engineering, cloud infrastructure, technical leadership, TDD practices, and game development insights.
---

## What's This All About?

This blog exists in the spirit of Austin Kleon's *Show Your Work* - documenting the messy, chaotic, tangent-filled reality of learning to build with AI.

You won't find polished tutorials here. Instead, you'll find:

- **The tangents** - like accidentally implementing Wave Function Collapse when you should be playtesting a board game
- **The failures** - five evenings lost to a refactor because the `.godot` folder was in git
- **The learning** - from AI skeptic to treating Claude like a junior engineer in four months
- **The meandering** - building 24k lines of Python for a game that probably should have been paper-prototyped first

**Why document this publicly?** Three reasons:

1. **For future me** - so I can remember what I learned when the details fade
2. **For you** - in case you're standing where I was in June, wondering "how does one actually vibe code?"
3. **For accountability** - nothing keeps you honest like documenting your scope creep in real-time

This isn't about showcasing expertise. It's about learning in public, sharing the process (not just the wins), and treating side projects as "learn how to AI" experiments rather than products.

If you're looking for clean, professional advice, my day job is Staff Engineering at The Economist. If you want to see what happens when curiosity meets AI-assisted development meets a nostalgic itch for a 90s RTS game... well, you're in the right place.

Welcome to the chaos.

---

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

{% if site.posts.size > 5 %}
## Post Archive

### All Posts
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
{% endif %}

## Subscribe & Stay Updated

- **RSS Feed:** [Subscribe to updates]({{ "/feed.xml" | relative_url }})
- **LinkedIn:** [Follow me for professional updates](https://linkedin.com/in/peter-van-onselen-a46b1b2b)
- **GitHub:** [See my latest code and projects](https://github.com/vanonselenp)

## Suggest a Topic

Have a topic you'd like me to write about? Questions about technology, development practices, or career advice? I'd love to hear from you! [Send me a message](/contact/) with your suggestions or questions.

---

*Thank you for reading! I hope you find these insights helpful in your own professional journey.*
