---
layout: post
title: "Scope Creep Chronicles: Creature Combat Devlog"
date: 2025-10-10 11:00:00 +0000
categories: personal board-game godot video-game claudecode codex vibecoding
---

_Crouching Creature Combat, hidden tangents..._

---

Combat is a cornerstone of the game’s core loop — it’s a wargame after all. If the creatures can’t attack or move, nothing else really works. So it felt like the perfect place to focus on getting one thing working at a time.

You know that feeling when you promise yourself to build *just one simple feature*… and then accidentally end up building half a combat system?
Yeah. That happened.

![current wip](/assets/scope-creep/current.png)

I set out to make creature movement and attack work. Just that. And technically… I did.

But also…

---

## So What Happened Since Last Time?

* Created a **test creature**
* Added **stubs for abilities** and creatures
* Can **play the creature onto the world**
* Creature can **move**
* Creature can **attack** (with a cheeky little “nudge” animation!)
* Creature is **persistent** in the world
* First version of a **combat system** is in place
* Height contributes to **defence**
* Combat uses **dice rolls**
* Added a **UI element** showing active units

Somewhere between “just movement and attack” and the inevitable barrage of scope creep that is this list… I may have overshot my initial scope a tiny bit.

---

## The Big Question I Didn’t Think Through

When I first added creature cards, I realised something obvious but important:

> “What happens to the card once the creature is played?”

Does it:

* 🃏 Get discarded like a one-off spell?
* 🏗️ Stay permanently on the battlefield, RTS-style?
* 🧍 Act more like an ally in [Marvel Champions](https://boardgamegeek.com/boardgame/285774/marvel-champions-the-card-game)?
* ❄️ Or a unique character like in [Undaunted](https://boardgamegeek.com/boardgame/268864/undaunted-normandy)?

I wasn’t sure which direction would be more fun, so I had a long chat with the AI to explore the implications of each — and in classic not-thinking-it-through fashion, this has the feeling of being a dramatic question that might shift the whole damn game all over again. Hello scope creep, my old friend. I’m trying to keep you in check this time, I promise — setting clearer boundaries for what belongs in the MVP and what gets kicked down the road for future me to deal with.

The key takeaway:
I want players to **get cards out fast**, **keep them on the board**, and **have those creatures feel unique**. So the “remove from deck” idea (like Undaunted) felt too punishing. RTS swarm spam didn’t fit either.

The sweet spot seems to be something like **Marvel Champions**: unique characters with meaningful impact.

---

## A Fun Rabbit Hole: Rewarding Combat

This led me to thinking: what happens when you **win** a combat?

That’s when [Battle Realms](https://store.steampowered.com/app/1025600/Battle_Realms_Zen_Edition/) came to mind — an underrated, vibey-as-hell RTS from way back, with samurai, werewolves, vampires, and mystical Eastern weirdness. It used combat to **generate resources for upgrades**.

I love that idea. It adds stakes and momentum to battles without punishing players for losing units. And in yet another stunning moment of self-realisation, I promptly undid all my changes related to this feature — because it was scope creep of the highest order!

---

## UI Tangents and Side Quests

UI clarity is what really shapes how the game *feels* to play, so making it intuitive is critical. When the interface gets in the way, the whole experience slows down, so I’ve been extra sensitive about how these elements work.

![creature movement](/assets/scope-creep/movement.png)

Of course, I also got distracted by UI.

Playing a card and then having it **disappear so you can see where to place it** just makes sense. So I ended up tinkering with creature display windows and UX polish far beyond what I planned. I also found myself wrestling with the active unit display — trying (and failing repeatedly) to get Claude and Codex to understand exactly what I wanted changed. It turns out it’s surprisingly difficult to use plain English to precisely specify how a UI element should behave.

But I did get a shiny radial menu for unit actions out of it…

![radial](/assets/scope-creep/radial.png)

---

## The Actual Goal? Achieved.

At the end of the day, I really did achieve what I set out to do:

✅ **Creature movement and attack** — working (ish)
🌀 Plus a whole lot of unexpected side questing, because game dev is never a straight line.

---

## Next Steps

Onward to the next rabbit hole.

This sprint was messy but productive — a reminder that even the tangents feed back into making the game feel more alive.

* Refine creature persistence and combat flow
* Continue working through the massive creature card spec doc — I barely made it through the first two abilities, and I still want to explore resource generation and upgrades from combat wins
* Keep iterating without accidentally building a full-blown RTS 😅

---

**TL;DR:**
I aimed for one thing. I built a small ecosystem. I’m proud, a little tired, and very excited about where this is going. And I’ve learned more about using AI tooling than I ever imagined.
