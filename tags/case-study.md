---
layout: page
title: Case studies
permalink: /tags/case-study/
description: Production stories with named incidents — what broke, why it broke, and what the feedback loop missed.
---

Production stories with named incidents. The trading engine that ran for forty-five minutes. The GDPR-shaped basket table that nobody had ever told to expire. The 280-file refactor that became unshippable. What broke, and what the feedback loop missed.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'case-study'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
