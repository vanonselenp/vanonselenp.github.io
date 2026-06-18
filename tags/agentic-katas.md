---
layout: page
title: Agentic katas
permalink: /tags/agentic-katas/
description: Posts on agentic katas — code-retreat-style practice for working with AI agents.
---

Code-retreat-style exercises for practising agentic coding. Deliberately ambiguous briefs with a privacy constraint and an extra-credit extension. The thing you build doesn't matter; the process does.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'agentic-katas'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
