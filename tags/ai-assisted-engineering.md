---
layout: page
title: AI-assisted engineering
permalink: /tags/ai-assisted-engineering/
description: Posts about working alongside AI agents — what changes about the craft, what stays stubbornly human, and what to encode rather than remember.
---

The craft posts. What actually changes when you work with AI tools every day, where the interesting failures live, and the small disciplines that keep production sane.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'ai-assisted-engineering'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
