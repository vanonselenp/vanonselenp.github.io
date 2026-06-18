---
layout: page
title: Topics
permalink: /tags/
description: Browse posts by topic — AI-assisted engineering, game development, the Bolt Action print pipeline, agentic katas, and more.
---

A different cut through the writing here. Threads on the blog page group by series; tags group by topic.

{% assign all_tags = "" | split: "" %}
{% for post in site.posts %}
  {% for tag in post.tags %}
    {% unless all_tags contains tag %}
      {% assign all_tags = all_tags | push: tag %}
    {% endunless %}
  {% endfor %}
{% endfor %}
{% assign all_tags = all_tags | sort %}

<ul class="tag-index">
{% for tag in all_tags %}
  {% assign tagged = site.posts | where_exp: "p", "p.tags contains tag" %}
  <li><a href="{{ '/tags/' | append: tag | append: '/' | relative_url }}">{{ tag | replace: '-', ' ' }}</a> <span class="tag-count">({{ tagged.size }})</span></li>
{% endfor %}
</ul>
