---
layout: page
title: Specs and process
permalink: /tags/specs-and-process/
description: Posts on spec-driven development, planning the work, and the disciplines that keep an AI-assisted process honest.
---

The boring stuff that makes the work go. Specs before code, plans that pre-decide one action per pull request, the disciplines that survive when context doesn't.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'specs-and-process'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
