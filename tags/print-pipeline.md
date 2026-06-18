---
layout: page
title: Print pipeline
permalink: /tags/print-pipeline/
description: The Bolt Action 3D print pipeline arc — concept to printable miniature, via ChatGPT, Meshy, and Bambu Studio.
---

The side project that turned into a process experiment: a chain of generative tools going from a concept image to a printable miniature. Two 1000-point armies so far.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'print-pipeline'" | sort: "date" %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
