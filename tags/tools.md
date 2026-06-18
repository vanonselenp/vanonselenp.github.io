---
layout: page
title: Tools
permalink: /tags/tools/
description: Posts about the tools behind the writing — harness-bench, print-bench, the zsh wrappers, and the plumbing in between.
---

Posts about the things I have built and use — harness-bench, print-bench, the zsh wrappers, and the plumbing in between. See also the [Projects](/projects/) page for repos.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'tools'" | sort: "date" | reverse %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
