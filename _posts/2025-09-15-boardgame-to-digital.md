---
layout: post
title: "I Just Wanted to Make a Board Game and Now There Are Procedural Islands"
date: 2025-09-07 11:00:00 +0000
categories: personal python board-game
---

_Why I Stopped Worrying and Learned to Love Chaos ...._

---

So… I’m supposed to be making a **board game**. At least, I think I am. Probably? Maybe?

What started as a simple idea about floating islands locked in war has slowly mutated into something far stranger.

---

### Where We Left Off

If you caught my last post, [Building AI Before Building the Game: A Cautionary Tale](https://www.petervanonselen.com/2025/09/07/building-ai-before-you-have-a-game/), you'll know I'd been trying to simulate *Sky Islands* in Pygame. The goal was to playtest the rules, track combat and control, and maybe get some balance insights. Then I got ambitious and plugged an LLM in to act as an AI player.

![silly ai](/assets/road_to_nowhere.png)

That went… poorly. The AI spent twenty straight turns building roads that went nowhere, while writing deeply convincing justifications for every decision. It was like watching a medieval city planner gone mad. Funny? Absolutely. Useful? Not so much.

---

### The Escalation: From Boring to Beautiful to Wild

After that fiasco, I stepped back and looked at my simulation. It worked, technically—but visually, it was about as inspiring as a spreadsheet. Dry. Functional. Boring.

I thought: *It just needs a little something ...*

So naturally I did the completely logical thing of iterating on the base concept, creating some physical components and playtesting the hell out of this... right? No.

Instead I:

* Downloaded Godot.
* Built a basic isometric grid.
* Added hexes stacked on other hexes.
* Added colours and a cloud-like background.
* Added roads.

![i might have a problem](/assets/boardgame-to-digital/color2.png)

And, then naturally, decided to throw in [**Wave Function Collapse**](https://www.youtube.com/watch?v=zE1Jbh8b0BM) for procedurally generated islands.

(Wave Function Collapse, for the unfamiliar: you feed an algorithm a set of tiles and rules for which tiles can sit next to which. It then generates new maps that look organic but still follow those constraints. Think Sudoku meets Minecraft.)

![waveform collapsing the hell out of this](/assets/boardgame-to-digital/waveform.png)

Each new step felt like a tiny, harmless addition—until I looked up and realized I was knee-deep in procedural generation instead of working on my board game.

---

### The Identity Crisis

At this point, I had to stop and ask myself ... what the hell am i doing?

* Am I still making a **board game**?
* Or is this now a **video game prototype** masquerading as a board game?

Because here’s where I stood:

* A physical prototype with real pieces, great for fast iteration.
* A digital build with pretty visuals, dynamic maps, and increasingly complex systems.

Two games. One idea. Total confusion.

---

### What I’m Learning About Chaos

Yes, there’s a certain logic to focusing purely on a physical prototype first. But this is a side project meant to be fun, and I honestly have no idea where it’s heading. So instead of forcing order, I’m leaning into the fun and seeing where it takes me.

Right now, chaos is bubbling everywhere because I’m basically doing both at the same time—tinkering with a paper version and iterating on a digital one.

And that’s not entirely unprecedented. Building a paper version of a game before implementing it digitally is a time‑honored tradition. One of the best tactics games I’ve played in years (Mario + Rabbids Kingdom Battle) was built this way, and it worked beautifully.

Here’s what I’m starting to realize:

* Building flashy visuals and complex systems is fun, but they’re *add-ons*, not the core of the game.
* Chaos is part of the creative process. The trick is knowing which parts to hold onto and which to let drift away.
* Having two prototypes isn’t inherently bad—as long as you know why each exists and what you’re testing with it.

---

### The Plan (For Now)

For now, I’m planning on following the fun—playing with procedural generation and trying to make this into a video game that can be played quickly.

And I might still be making a physical version because drawing is fun and making physical things is entertaining from time to time.

...yes, I know I just went, "I am going to do everything everywhere all at once..."

---

### Embracing the Weirdness

![where i am so far](/assets/boardgame-to-digital/final.png)

Maybe this project was never going to stay neat and tidy. Maybe my creative process just looks like a cloud of floating hexes.

And maybe that’s okay.

So, here’s to embracing chaos, even when you’re not entirely sure what the hell you’re building.

  <iframe width="100%" height="315" src="https://www.youtube.com/embed/Xo7D7lnq_zQ?si=70eiCuDIwS0SaNHG" title="YouTube video player" frameborder="0" 
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
  referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style="max-width: 100%;"></iframe>
