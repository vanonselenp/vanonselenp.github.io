---
layout: post
title: "How Many Times Do You Have to Build Too Much to Learn Scope Creep?"
date: 2025-11-20 08:00:00 +0000
categories: godot vibecoding claudecode specdrivendevelopment
---

_Scope Creep Keeps Teaching Me..._

---

![banner](/assets/no-energy-week/banner.png)

# Scope Creep Keeps Teaching Me

Have you ever had one of those weeks where you suddenly have to be traveling a lot and don't really have any time for personal projects? This has been my week. I still managed to get two creatures and six abilities created.

The Flux Chaos controls the board by moving creatures into and out of position, swapping them from behind enemy lines or randomly teleporting them somewhere (maybe even off into the void). The Flux Storm does massive area damage while locking down the area preventing anyone from teleporting in and out. Watching these creatures interact with the existing systems is delightful. The abilities are beginning to feel like they synergize and interact together nicely.

I've been on a mission to prototype this strange game idea for a while now. I started the repo on September 4th. Three months later, I'm watching a prototype that's actually starting to feel like a game with interesting systems.

## But here's what I should have learnt sooner: I didn't cut far enough.

When I started, I aggressively removed things. All 8 envisioned factions. The single-player campaign, stories, and lore. AI players. Multiplayer. Different form factors like mobile. Complex models and animations. I thought I'd solved the scoping problem. Oh how innocent I was.

I then built ten creatures with twenty-nine abilities. I added procedural island generation and dynamic road construction. I went down tangents and rabbit holes as I iterated from RTS-style UI to pure card-driven gameplay.

Looking at that list now, that should have been a warning sign. And it gets worse: my remaining feature list for MVP includes five more buildings, five more spells, multiple win conditions, fog of war, proper turn behavior, UI polish.

It's only now that I am looking at my remaining feature list (I wrote up the list for this very blog post), that I realize the entirely obvious thing. I am _still_ overscoping. Scope creep doesn't stop after one round of cuts. It's persistent. Even when you're actively trying to think in MVP terms, there's a pull to add one more building, one more spell, one more system. Each one feels necessary. But they compound.

I should have picked this up sooner with that grinding feeling. I have been having with the creatures and abilities. It has felt like motivation leeching away in the never ending drudgery. It was a clear warning sign I was off the path.

So what should the real MVP actually be? **One or two creature types. A handful of abilities. One building. One spell. Island control. Prove it works, then iterate.**

Instead, I've been building toward a feature-complete prototype when I should be building toward the **smallest** thing that proves the game is playable and interesting.

So here's my actual MVP: one spell (meteor), Fog of War, one win condition, UI, and two decks. Nothing more! Just the core systems missing, playable, shippable.

## The lesson keeps teaching itself

There's a valuable lesson here about scope discipline. I thought I'd learned it when I cut factions and campaigns. But you keep learning it, over and over, if you're paying attention. Every time you build something, you get a clearer picture of what actually matters. And every time, you realize you could have cut further.

The game is starting to have shape because I've been building and learning. But I'm also learning—again—that shipping something small and real beats shipping something comprehensive and theoretical. Time to cut deeper. And I need to get a prototype finished before adding a single feature more.