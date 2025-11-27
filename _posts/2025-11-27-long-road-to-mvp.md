---
layout: post
title: "The Long Road to MVP"
date: 2025-11-27 08:00:00 +0000
categories: godot vibecoding claudecode specdrivendevelopment
---

_How I learned to stop overthinking and ship the damn thing..._

---

![banner](/assets/long-road/banner.png)

[Last week I had a sudden but inevitable realisation](https://www.petervanonselen.com/2025/11/20/scope-creep/). Basically my MVP was completely not an MVP but rather a bloated over-built system that I should have been moving to release sooner. Which in hindsight I should have realised... 4 weeks ago. Lesson learned.

So, this week I started with yet another plan where I detailed out a new spec that broke down the exact things I needed to do. And then... I did just that! Everything else is deferred.

**Broad plan for MVP:**
- 1 Spell: Meteor (DONE)
- 1 Victory condition: own all the islands - IN PROGRESS
- 2 Unique Decks: TODO

The spell was easy. Just another ability, and make it bigger, cost more and have an animation that then removes a massive amount of real estate. Big, flashy, simple.

![meteor](/assets/long-road/meteor.gif)

The victory condition, however, has turned into a far more crunchy problem. Turns out wiring up ownership, health tracking, and win conditions across multiple systems was messier than I thought. I've built:
- A game over screen to start a new game
- Health on the core island node
- A UI display to see that health
- A manager to track who owns the islands and a way to change ownership
- A victory condition that checks each round if someone's actually won

Almost there! The missing piece is creatures targeting the core island and dealing damage to it. Once I wire up that damage pathway, the whole system clicks. That's what I'm grinding through at the moment.

All that will be left is two decks. Which should be as simple as updating two config files, and I'll have a playable MVP. Finally.

![light](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExOG05YndpM2NxbWIxaDE5N2t0ODg2NDRia29tdWd0OXhoaXViMTFhaSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/dyw4fuAhPaIh0japgg/giphy.gif)