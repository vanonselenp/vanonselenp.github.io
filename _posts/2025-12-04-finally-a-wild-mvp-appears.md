---
layout: post
title: "Finally... A Wild MVP Appears"
date: 2025-12-04 08:00:00 +0000
categories: godot vibecoding claudecode specdrivendevelopment
---

_Three Months to MVP: What I Learned Building a Tactical Card Game with AI..._

---

![banner](/assets/mvp/banner.png)

It's been three months since I started trying to make Horizon's Edge, a tactical turn-based wargame in the sky. And honestly, I'm completely stunned that I even have something that actually ... kinda ... works.

## From Vibe to Spec

When I started this project, I was pure vibe coding. But somewhere in the middle, when I was trying to refactor the UI from a classic RTS/turn-based strategy with a mass of buttons to something entirely driven by card play, vibe coding hit a wall. I couldn't get AI tooling to cooperate with my loose intuitions. That's when I started working with specs and it changed my life.... metaphorical life .... but life!

![card driven](/assets/mvp/cards.png)

Writing a clear specification before diving head first into a vibe changed everything. Suddenly the AI had guardrails. It stopped looping in circles. If you want to go deeper on this, I wrote about starting to figure out specs in [Chaos, Cards, and Claude](https://claude.ai/2025/10/03/chaos-cards-and-claude-copy/).

## Months of Education

What I've learned so far is this: it's entirely possible to make working software with AI tools. You can keep momentum even when you're completely out of energy or time. But the most important thing ... the thing that actually matters ... is that you have to always verify what the AI outputs. Automated unit tests are your best friend here. A Quality first mindset and thinking about edge cases is fundamental.

![waveform generation](/assets/mvp/waveform.gif)

I've done major refactors. I've rethought how the game works multiple times. I added procedural generation because it was fun. I figured out how to make the game work with just card play mechanics that... mostly work (much to my surprise). Some refactors were vibe-coded disasters; others were spec-driven and clean. But every single one taught me something about how to work with AI as a tool rather than a replacement.

## The MVP: What It Took

Two days ago I finished the final major system needed to validate the MVP: the victory system. Islands needed to change ownership. Every existing system needed to integrate with that. Core island nodes needed to be targetable from creatures, spells, and abilities. Getting the targeting code to work meant hitting more touch points than I anticipated. A lot of different abilities needed specific ways to target islands, not just creatures. It was more entertaining than expected, but I had a spec, and that spec kept me honest.

I now have two thematic decks that are actually unique. 10 creatures. Infrastructure cards that terraform and change the world. A spell that destroys the world. Card play mechanics that mostly work. A whole horde of nuanced and detailed rules about damage and combat that work. 

**Prototype done. Well, mostly.**

The mechanics are all there. What's left is UI feedback. Cards need to show their play cost clearly, what they do when discarded, what abilities they have before you play them. I know all this because I've spent three months building it. Others won't. So I'm going to tackle those UI gaps this week, then put this in front of a few people to get real feedback.

## Now It's Your Turn

I've spent the past five months working on this. It started with a Magic the Gathering Pauper Jumpstart cube that just wouldn't get out of my head, went running headlong into a board game prototype that was way too complicated and barrelled straight into this game. I've learned a ridiculous amount. **But here's what actually matters:**

It is possible to make working software with AI. You can make some amazing things with these tools. You can learn as you go. You can ship those crazy ideas you never thought you could.

**So here's what I want:** 

I want *you* go out and make your own mistakes. Build something weird. Use AI as a tool, verify everything it does, and then make something great. Make art. Because making art, well, that's the most human thing we can do.

Tell me what you build. I want to hear about it.

Till then, keep learning.

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="https://www.youtube.com/embed/NdQgOLlt8QQ?si=F2rdwci0GcDvNm9R" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>