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

- [Islands at War: Designing a Board Game with AI](/2025/08/21/sky-islands/) — August 2025
- [I Just Wanted to Make a Board Game and Now There Are Procedural Islands](/2025/09/07/boardgame-to-digital/) — September 2025
- [Building AI Before Building the Game: A Cautionary Tale](/2025/09/07/building-ai-before-you-have-a-game/) — September 2025
- [When Refactors Eat Your Game (and Your Evenings)](/2025/09/29/the-grand-refactor/) — September 2025
- [Cards, Chaos and the subtle art of Claude Code](/2025/10/03/chaos-cards-and-claude-copy/) — October 2025
- [Scope Creep Chronicles: Creature Combat Devlog](/2025/10/10/scope-creep-chronicles/) — October 2025
- [The Road to Combat Is Paved with Tangents](/2025/10/17/road-to-combat-paved-with-blink/) — October 2025
- [I Actually Stayed On Task (For Once)](/2025/10/24/i-stayed-on-task/) — October 2025
- [The Beautiful Boring: How I Refactored a Game Without Breaking it](/2025/11/06/a-chill-refactor/) — November 2025
- [How to Get Things Done When You Have Nothing but Process](/2025/11/13/the-no-good-low-energy-week/) — November 2025
- [How Many Times Do You Have to Build Too Much to Learn Scope Creep?](/2025/11/20/scope-creep/) — November 2025
- [The Long Road to MVP](/2025/11/27/long-road-to-mvp/) — November 2025
- [Finally... A Wild MVP Appears](/2025/12/04/finally-a-wild-mvp-appears/) — December 2025

</details>

<details class="thread-section" markdown="1">
<summary>

AI-Assisted Engineering — the craft

<p class="thread-description">What actually changes when you work alongside AI agents every day. Specs, verification, katas, and knowing when to slow down.</p>

</summary>

- [From AI Skeptic to Constant Collaborator](/2025/10/20/what-i-have-learnt/) — October 2025
- [AI Spec Driven Development](/2025/10/30/exert-of-what-i-learnt/) — October 2025
- [The Boring Path to Actually Shipping with AI](/2025/10/31/boring-path-to-shipping/) — October 2025
- [Why You Shouldn't Speedrun a Production Refactor](/2025/12/12/speedrunning-prod-refactors/) — December 2025
- [This Is the Way: Delete the Code](/2026/02/10/agentic-play/) — February 2026
- [14 PRs, 6 Repos, 1 Button: A Tale of Tumbling Down the Rabbit Hole](/2026/02/12/rabbit-holes/) — February 2026
- [How I Learnt to Stop Worrying and Love Agentic Katas](/2026/03/05/learn-to-love-agentic-coding/) — March 2026
- [The Feedback That Doesn't Care About Your Title](/2026/03/05/the-feedback-that-doesnt-kill-you/) — March 2026
- [The Smell of Panic When You Context Thrash](/2026/03/24/the-smell-of-panic-while-you-thrash/) — March 2026
- [The Council Will See You Now...](/2026/04/03/the-council-will-see-you-now/) — April 2026
- [The Grand Plugin Trap](/2026/04/11/the-grand-plugin-trap/) — April 2026
- [The Canary in the Harness](/2026/04/12/the-inevitable-lobotomisation-of-claude/) — April 2026
- [Conscious Coverage](/2026/04/16/concious-coverage/) — April 2026

</details>

<details class="thread-section" markdown="1">
<summary>

Career & Meta

<p class="thread-description">Staff engineering, career thinking, and why this blog exists.</p>

</summary>

- [A Blog of Dubious Intent](/2025/08/01/a-blog-of-dubious-intent/) — August 2025
- [What Does a Staff Engineer *Actually* Do?](/2025/08/02/staff-engineer/) — August 2025
- [Charting a Path to Senior Staff Engineer](/2025/08/03/senior-staff-engineer/) — August 2025
- [The Zero-to-Vibe Coding Jumpstart Cube Catastrophication](/2025/08/04/jumpstart-cube-catastrophication/) — August 2025
- [I Built This In A Prompt Window! With A Box Of Filament!](/2026/04/22/vibe-coding-reality/) — April 2026

</details>

---

## All posts

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
