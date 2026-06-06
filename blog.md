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

- {% include post-listing.html url="/2025/08/21/sky-islands/" %}
- {% include post-listing.html url="/2025/09/07/boardgame-to-digital/" %}
- {% include post-listing.html url="/2025/09/07/building-ai-before-you-have-a-game/" %}
- {% include post-listing.html url="/2025/09/29/the-grand-refactor/" %}
- {% include post-listing.html url="/2025/10/03/chaos-cards-and-claude-copy/" %}
- {% include post-listing.html url="/2025/10/10/scope-creep-chronicles/" %}
- {% include post-listing.html url="/2025/10/17/road-to-combat-paved-with-blink/" %}
- {% include post-listing.html url="/2025/10/24/i-stayed-on-task/" %}
- {% include post-listing.html url="/2025/11/06/a-chill-refactor/" %}
- {% include post-listing.html url="/2025/11/13/the-no-good-low-energy-week/" %}
- {% include post-listing.html url="/2025/11/20/scope-creep/" %}
- {% include post-listing.html url="/2025/11/27/long-road-to-mvp/" %}
- {% include post-listing.html url="/2025/12/04/finally-a-wild-mvp-appears/" %}

</details>

<details class="thread-section" markdown="1">
<summary>

AI-Assisted Engineering — the craft

<p class="thread-description">What actually changes when you work alongside AI agents every day. Specs, verification, katas, and knowing when to slow down.</p>

</summary>

- {% include post-listing.html url="/2025/10/20/what-i-have-learnt/" %}
- {% include post-listing.html url="/2025/10/30/exert-of-what-i-learnt/" %}
- {% include post-listing.html url="/2025/10/31/boring-path-to-shipping/" %}
- {% include post-listing.html url="/2025/12/12/speedrunning-prod-refactors/" %}
- {% include post-listing.html url="/2026/02/10/agentic-play/" %}
- {% include post-listing.html url="/2026/02/12/rabbit-holes/" %}
- {% include post-listing.html url="/2026/03/05/learn-to-love-agentic-coding/" %}
- {% include post-listing.html url="/2026/03/05/the-feedback-that-doesnt-kill-you/" %}
- {% include post-listing.html url="/2026/03/24/the-smell-of-panic-when-you-context-thrash/" %}
- {% include post-listing.html url="/2026/04/03/the-council-will-see-you-now/" %}
- {% include post-listing.html url="/2026/04/11/the-grand-plugin-trap/" %}
- {% include post-listing.html url="/2026/04/12/the-inevitable-lobotomisation-of-claude/" %}
- {% include post-listing.html url="/2026/04/16/concious-coverage/" %}
- {% include post-listing.html url="/2026/05/04/your-scientists-were-preoccupied/" %}
- {% include post-listing.html url="/2026/05/06/show-your-work/" %}

</details>

<details class="thread-section" markdown="1">
<summary>

Career & Meta

<p class="thread-description">Staff engineering, career thinking, and why this blog exists.</p>

</summary>

- {% include post-listing.html url="/2025/08/01/a-blog-of-dubious-intent/" %}
- {% include post-listing.html url="/2025/08/02/staff-engineer/" %}
- {% include post-listing.html url="/2025/08/03/senior-staff-engineer/" %}
- {% include post-listing.html url="/2025/08/04/jumpstart-cube-catastrophication/" %}
- {% include post-listing.html url="/2026/04/22/vibe-coding-reality/" %}
- {% include post-listing.html url="/2026/05/10/an-army-of-one-prompt/" %}

</details>

---

## All posts

{% for post in site.posts %}
- {% include post-listing.html post=post %}
{% endfor %}
