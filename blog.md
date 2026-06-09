---
layout: page
title: Blog
permalink: /blog/
description: Posts about AI-assisted development, game development with Godot, agentic katas, and the craft of working alongside AI agents.
---

<details class="thread-section" markdown="1">
<summary>

Horizon's Edge — the game dev journey

<p class="thread-description">Building a tactical wargame in Godot with AI assistance. Started as a board game. Escalated.</p>

</summary>

{% assign gamedev_posts = site.posts | where: "thread", "gamedev" | sort: "date" %}
{% for post in gamedev_posts %}
- {% include post-listing.html post=post %}
{% endfor %}

</details>

<details class="thread-section" markdown="1">
<summary>

AI-Assisted Engineering — the craft

<p class="thread-description">What actually changes when you work alongside AI agents every day. Specs, verification, katas, and knowing when to slow down.</p>

</summary>

{% assign craft_posts = site.posts | where: "thread", "craft" | sort: "date" %}
{% for post in craft_posts %}
- {% include post-listing.html post=post %}
{% endfor %}

</details>

<details class="thread-section" markdown="1">
<summary>

Career & Meta

<p class="thread-description">Staff engineering, career thinking, and why this blog exists.</p>

</summary>

{% assign meta_posts = site.posts | where: "thread", "meta" | sort: "date" %}
{% for post in meta_posts %}
- {% include post-listing.html post=post %}
{% endfor %}

</details>

---

## All posts

{% for post in site.posts %}
- {% include post-listing.html post=post %}
{% endfor %}
