---
layout: page
title: Topics
permalink: /tags/
description: Browse the writing by series (the arcs) or by topic (cross-cutting tags) — AI-assisted engineering, game development, the Bolt Action print pipeline, agentic katas, and more.
---

Two cuts through the writing: by **series**, which follows each arc, and by **topic**, which groups across them. The [blog](/blog/) is the plain chronological view.

## By series

{% assign thread_order = "craft,gamedev,meta" | split: "," %}
{% for t in thread_order %}
{% assign thread_posts = site.posts | where: "thread", t %}
{% if thread_posts.size > 0 %}
{% case t %}
{% when "craft" %}
### AI-assisted engineering

{% assign blurb = "What actually changes when you work with AI tools every day, where the interesting failures live, and the small disciplines that keep production sane." %}
{% assign ordered = thread_posts | sort: "date" | reverse %}
{% when "gamedev" %}
### Horizon's Edge

{% assign blurb = "The game-dev devlog: a tactical wargame in Godot that began as a board game and grew legs. In order, so the arc reads start to finish." %}
{% assign ordered = thread_posts | sort: "date" %}
{% when "meta" %}
### Side projects &amp; meta

{% assign blurb = "Where it started (a Magic: The Gathering cube), the Bolt Action 3D-print pipeline, and why this blog exists." %}
{% assign ordered = thread_posts | sort: "date" | reverse %}
{% endcase %}
_{{ blurb }}_

{% for post in ordered %}
- {% include post-listing.html post=post %}
{% endfor %}
{% endif %}
{% endfor %}

## By topic

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
