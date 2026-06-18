---
layout: page
title: Blog
permalink: /blog/
description: Posts about AI-assisted development, game development with Godot, agentic katas, and the craft of working alongside AI agents.
---

## All posts

{% for post in site.posts %}
- {% include post-listing.html post=post %}
{% endfor %}
