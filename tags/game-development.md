---
layout: page
title: Game development
permalink: /tags/game-development/
description: The Horizon's Edge devlog — a tactical wargame in Godot that started as a board game and grew legs, then a hex grid, then procedural maps.
---

The Horizon's Edge devlog. Floating islands, hex grids, Wave Function Collapse, refactors I could probably have skipped. Posts in chronological order so the arc reads start to finish.

{% assign tagged = site.posts | where_exp: "p", "p.tags contains 'game-development'" | sort: "date" %}
{% for post in tagged %}
- {% include post-listing.html post=post %}
{% endfor %}
