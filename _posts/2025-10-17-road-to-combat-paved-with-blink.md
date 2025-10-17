---
layout: post
title: "The Road to Combat Is Paved with Tangents: A Devlog"
date: 2025-10-17 08:00:00 +0000
categories: personal board-game godot video-game claudecode codex vibecoding
---

_I set out to make a combat system. I returned with roads, models, and a blink ability..._

---

# Tangents, Roads, and Blinking Archers

okay okay okay, so I *know* last time I was all:

> “I am going to work on the combat system.”

and I meant it. I really did.

I started the week’s development figuring out how to get a second creature working — this time one that could *shoot*! and it shot! with animation! and a lovely red number floating overhead when it hit.

Then I spent some time trying to convince the AI to make an archer… which came out as a cylinder and a torus mashed together like some long-lost relic from *Lord of the Rings*.

![archer](/assets/road-to-combat/archer.png)

Somewhere between the floating numbers and cursed geometry, I ran into a movement bug where the creature could only move *upwards* but never *downwards* — so, you know, just another normal day working on a game with a super-powered AI as a pair.

And that’s the problem with having a super-powered AI as a pair: it is *beyond* exceedingly simple to wander off on completely unrelated tangents. Which is, of course, what I did.

---

## The Tangent: Shiny Hexes ✨

When I was working through a game dev course on [Jumpstart to 2D Game Development: Godot 4.4+ for Beginners](https://www.udemy.com/course/jumpstart-to-2d-game-development-godot-4-for-beginners/) last year, I came across a really cool site: [kenney.nl](https://kenney.nl/).

They’ve got models, textures, and all sorts of game assets. And wouldn’t you know it, I found a bunch of hex models that perfectly matched the vibe in my head.

And just like that, all thoughts of combat systems and specs and rational planning *evaporated*.

No, now was *obviously* the perfect time to get models and textures in. So I immediately downloaded the GLB files and started plugging them into my wave function collapse algorithms.

![current](/assets/road-to-combat/current.png)

Instant vibe shift. The world suddenly *looked* like something. I’m not using all the models yet… but give me time 😄.

---

## The Roads to Madness 🛣️

With proper models in hand, I finally turned to something that’s been quietly tormenting me for weeks: roads.

Now that I had actual path models to work with, I thought this was going to be a cinch.

Nope. No. Oh hell no.

This is the kind of task that is *inherently infuriating* to get an AI to handle. Its sense of direction doesn’t match the way the world is rendered, and trying to explain rotations in a way that makes sense to both of us is like trying to teach a goldfish to drive.

![roads roads roads](/assets/road-to-combat/roads.png)

And if the AI ever *accidentally* gets something right, it will immediately overwrite it in the next change. Because of course it will.

My eventual workflow:

* Get the AI to build the big stuff — toggles, switches, base structure.
* Then manually go through and tweak everything myself.

Thank god for Git and my obsession with [save scumming](https://tvtropes.org/pmwiki/pmwiki.php/Main/SaveScumming) my way back to a sensible state.

---

## Meanwhile… Combat System? 🫣

Hang on though.
Wasn’t I working on a *combat system*?
Damn it.

Okay, where was I?

Ah yes — my ever-growing planning folder to the rescue.

I’ve developed a habit of getting the AI to output the result of any long feature discussion into a spec or planning file that gets committed into the repo.

Which is how I ended up with… about a dozen specs.

Some were implemented, some were “I realized this was a tangent and saved myself,” and some were very much still alive. After some reorganizing, I was down to a high level planning doc and a solid todo list that was a solid active plan.

```
➜  horizons-edge git:(main) ✗ ls planning/6-
6-implementation-todo.md
6-test-deck-archetypes-energy-abilities.md
```

Then came the fun part: getting the AI to validate how accurate my current TODO list was against the plan — and then, obviously, not trusting it at all and just starting to build anyway 😄.

---

## Back on Track: Blink ✨

At last, *finally*, I was back on combat system track.
And the first order of business: give my test creature a **blink ability**.

![blink ability!](/assets/road-to-combat/radial.png)

Let’s see how far I get next week.

Until then, I hope you’re enjoying whatever tangent is currently distracting you from your side project. I salute you, fellow tangent adventurers. 🫡

---

## 📝 Progress Summary Since last time.

* 🚧 **Road System:** Added straight roads, corners, intersections, and 3–5-way connections. Complex rotation logic, road-to-hex connectivity.
* 🧱 **3D Asset Library:** Integrated Kenney Hexagon Kit (180+ models, textures, documentation).
* 🏹 **Combat & Abilities:** Projectile system, Archer & Scout cards, ability system improvements, radial menu, energy planning.
* 🖱 **Input & UI:** New input controller with hex highlighting, better radial menu, multiplayer safeguards, grid visualization.
* 🧭 **3D Model Integration:** `hex_tile_model_config.gd`, updated rendering, road path visualization.
* 🗂 **Documentation:** New spec for energy payment (spec 7), reorganized planning docs.
