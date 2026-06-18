---
layout: page
title: Career and meta
permalink: /tags/career-meta/
description: Staff engineering, career thinking, and why this blog exists.
---

Staff engineering, career thinking, and the meta posts about why this blog exists in the first place.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'career-meta'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
