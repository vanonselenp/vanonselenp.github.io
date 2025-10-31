---
layout: post
title: "When Refactors Eat Your Game (and Your Evenings)"
date: 2025-09-29 11:00:00 +0000
categories: personal python board-game godot video-game
---

_From Buttons to Cards: A Sideways Journey_

---

# The Grand Refactor!

![current look](/assets/grand-refactor/current.png)

[Last time we chatted](https://www.petervanonselen.com/2025/09/07/boardgame-to-digital/) I was making excellent progress with the video game implementation of a board game I'm randomly working on. I had island placement, roads, chunking, waveform-collapse procedural generation. It was smoking. I was learning how to get Claude to code well. The way of the Force was strong.

And then I ran a little terminal command:

```bash
$ git ls-files | grep '\.gd$' | xargs wc -l
```

…and what I saw was a bunch of files well over 2k lines. Clearly I’d missed a refactor cycle (or three).

Meanwhile, I’d spun up a Claude sub-agent to do research on tech topics. Naturally, one of the first queries was: *“best practices for Godot.”*

The results:

* Use a signal-based architecture (which matched my half-remembered notes from a Godot course last year).
* Use singletons for global access and cross-cutting concerns like game managers and event buses.
* And, buried near the bottom as a tiny afterthought: *“Do not include the `.godot` directory in your repo.”*

Guess what I had in my repo.

![the inevitable betrayl](/assets/grand-refactor/betrayal.png)

I deleted the folder… and unleashed a week of refactor drama. Turns out the AI had written multiple cyclic dependencies that only “worked” because the cache made it look fine.

Cue the AI loop:

* *“To fix cyclic deps, remove types.”*
* *“No wait, add types.”*
* *“Think harder.”*
* *“Ultra-think.”*

This went on for hours until I forced a combo:

* do ultrathink,
* do not remove types,
* change the dependency pattern,
* refactor large files into smaller files.

That finally got things moving. Between Claude and Codex, the refactor slogged forward. But it cost me five evenings of work. 

When the dust cleared, I… immediately rethought the UI.

Up to now, core gameplay actions (building islands, adding chunks, placing roads and buildings) were just buttons. Cards existed, but only for creatures and spells. Then I thought: *what if everything was a card?*

![wrieframes](/assets/grand-refactor/wireframe.jpeg)

That would unify the control system: play a road, play an island, play a creature — all from cards. It lays the groundwork for an MVP, and it leans into what I love about games like [Undaunted](https://boardgamegeek.com/boardgame/268864/undaunted-normandy) and [Memoir ’44](https://boardgamegeek.com/boardgame/10630/memoir-44), where your options each turn come from your hand.

So naturally, I dove straight into a UI refactor.

At least this time I started with wireframes in my sketchbook, thinking mobile-first. Right now the UI shows:

* your resources,
* your current hand of cards,
* a test deck with only the working cards,
* and the ability to create islands by playing cards and paying with other cards.

To call this “progress” would be… generous. It’s more of a profound sideways move. But that’s coding sometimes — discovery through chaos.

The one genuinely new thing I’ve started doing is **feature planning with Claude**. Basically it goes like:

* I describe the feature
* Claude grills me with clarifying questions
* I save that Q&A as documentation
* then Codex implements
* Claude reviews.

Complete aside: I also started playing with OpenAI’s Codex to see what it’s like. Codex feels like an agent you hand a ticket to and then 30 minutes later it drops a PR on your desk. Claude, on the other hand, is more like a junior dev you pair with — lots of back-and-forth, explaining, nudging, but it stays with you in the problem.

This flow has meant:

* less back-and-forth,
* better documentation,
* and an easier way to track what I’m actually building.

Which is good, because this project has been the wildest, flux-crazed coding ride I’ve ever been on.

![cards cards cards](/assets/grand-refactor/cards.png)

---

## What’s next

Honestly? No idea. Probably “make more cards actually work.” and "make them look more informative than tiny text you got to squint at to figure out what you are trying to do!"

Right now I’m wrestling the **road network** into the card system. The “play a card → build roads” flow keeps fighting me. It *works* as a button; it *sulks* as a card.

Near-term plan (aka cope notes):

* **Make roads a first-class action.** Card triggers a `BuildRoadNetwork` action with inputs (start, end, cost), not a kitchen-sink utility.
* **Signals over reach-ins.** Card emits “build-road-requested”; the road system owns the how.
* **Pay-before-play.** Validate cost and constraints first, then build; if it fails, no state touched.
* **Isolate the graph.** Get road-graph ops (connectivity, loops, costs) tested in isolation so I’m not debugging UI + rules at once.
* **Tiny wins.** One card → one road segment → then chains → then networks.

If that behaves, I’ll circle back and keep converting the old button-y stuff into cards until the whole game flows from a hand. If it doesn’t… I will perform ritual sacrifices to the debug gods and try the other other thing.
