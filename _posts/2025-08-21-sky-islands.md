---
layout: post
title: "Islands at War: Designing a Board Game with AI"
date: 2025-08-21 11:00:00 +0000
categories: personal python board-game
---

---

About two weeks ago I wrapped up a project that had completely consumed me: figuring out how to create a Jumpstart cube from a Pauper cube (I wrote about that here: [Jumpstart Cube Catastrophication](https://vanonselenp.github.io/2025/08/04/jumpstart-cube-catastrophication/)). For a few weeks it was all I thought about in my spare time — basically just spent every free moment vibing on it, even when I was watching a TV show with my wife. But while I was busy tweaking code to generate decks, extract themes, and balance relative deck strengths, another idea was quietly percolating in the back of my mind.

---

### Inspiration: Rediscovering NetStorm

It started with a simple question: *do you remember NetStorm?*

![Netstorm in action](/assets/netstorm.png)

For most people, the answer is no. [NetStorm](https://www.netstormhq.net/) was a quirky real-time strategy game from the late 90s where players built chains of bridges to connect floating islands, deployed priests to capture enemy units, and unleashed elemental spells to control the battlefield. Matches were fast, tactical, and strange in a way that made it unforgettable, even if few played it at the time.&#x20;

But for me, it triggered an itch that just couldn’t be scratched. For the past year it’s been popping into my head like a song that gets stuck on repeat — especially the memory of floating islands, the roads stretching between them, and the chaos that ensued once those bridges connected. And since it’s impossible to play on modern tech without resorting to figuring out complicated emulation for a legacy Windows game on a modern Mac, I found myself wondering: what if I could capture that vibe from a board game instead?

It was a ridiculous idea in some ways, rooted in nostalgia for something obscure. But it stuck. And once the cube project was done, I found myself diving headfirst into a new design challenge. This time, though, I wasn’t working alone.

---

### Lessons from the Cube Project

The Jumpstart cube project had taught me something important: **AI could be a collaborator, not just a tool.**

The breakthrough wasn’t about the right prompt or the cleverest model hack. It was about treating the AI like a **junior engineer** — someone who could help generate ideas, point out problems, and accelerate iteration, but who still needed guidance, context, and decisions.

I learned to:

* Ask AI to critique ideas, not just produce them.
* Frame questions in terms of gaps, edge cases, and “what doesn’t make sense.”
* Use the back-and-forth to sharpen my own intent.

That mindset became the foundation for the new board game project.

---

### From Digital to Tabletop: Goals and Challenges

The initial vision that drove me was the feeling of **islands floating in the sky at war** — a mashup of inspirations:

* Magic: The Gathering’s **Jumpstart** ease of deck building and fun with interesting themed decks,
* Marvel Champions’ **card management**,
* and Star Wars: The Deckbuilding Game’s **capital ships** — which at first felt like they could fit the vibe I was imagining, but in my version, those ships were islands.

I started with a speculative chat that led to a rough design doc — high-level, but with enough of a skeleton to start iterating toward a solution. Then I followed it up with discussions about resource management, card flow, and how creatures might interact with the islands.

At each stage I translated these prompts ithrough Claude Code into a sprawling Python codebase, building rough but tangible systems so I could test how the mechanics meshed and influenced each other.

And then came the breakthrough .... or perhaps it was a bombshell. This was the small decision that went on to change every other single decision, as the consequences kept cascading out from it.

---

### The Sky Island Moment

The question that changed everything was deceptively simple: *what exactly are the islands, thematically?*

Somewhere in that back-and-forth, the idea of **sky islands** emerged. The idea went from an abstract hand wave of “there is a thing” to grappling with how to tie them into gameplay — what does it mean to interact with them, and why does that even matter? Suddenly the game wasn’t just a dueling card game. It shifted into something closer to a **dueling wargame** — a clash of floating fortresses, each vying for control of the skies.

That one shift cascaded into every corner of the design:

* **Creatures** became more than just units — they had roles tied to the islands themselves.
* **Resources** weren’t just mana, they were generated through interactions between creatures, cards, and island abilities.
* The **turn structure** morphed to resemble wargames like *Bolt Action* or even the action phases of *Terraforming Mars*.
* The definition of the **“player” avatar** in the game changed, along with how victory was determined.

It was dramatic. The feel of the entire game had transformed. And it had all come out of a collaborative conversation with the AI.

---

### How Collaboration Looked in Practice

One of the things I’ve been experimenting with is using **different AIs for different roles**. For this project:

* I’d often workshop prompts and do deep exploratory discussions in **ChatGPT**, digging into mechanics and edge cases.
* Then I’d switch to **Claude** when it came time to pair on writing code or fleshing out structured text.

```
~ ls ~/workspace/sky-islands/specs
1-initial-feature.md              14-streamline-resources.md        5-creatrure-combat.md
10-resource-management.md         15-streamline-upkeep.md           6-turn-structure.md
11-indepth-turn-structure.md      2-pay-by-discard.md               7-leader-homebase.md
12-upkeep-payment-supply-lines.md 3-sky-islands.md                  8-victory-conditions.md
13-deck-composition.md            4-ui.md                           9-hand-size-and-draw-mechanics.md
```

The rhythm became clear: spend more time up front in detailed conversation about a single feature or mechanic, then move to execution.

The most valuable questions I asked were:

* *Where are the gaps?*
* *What doesn’t make sense?*
* *What’s wrong with this design?*

Those questions made the AI less of an idea generator and more of a **critical partner**. And that’s when the collaboration felt most real.

---

### Where I Am Now

At this point, I have a **partially refined board game** with a comprehensive set of rules that cover deck design, map interaction and play, resources, hand management, combat, magic, and more. I also have a **partially implemented working Pygame simulation** of the board game. It’s still very much a developer interface and only kind of works, but it’s there. It’s already over 24k lines of Python code.

![Sky islands in action!](/assets/skyisland.png)

What’s exciting is how the different systems impact each other in ways that feel earned and interesting — at least from my high-level thinking so far. I don’t yet have a fully functional version of the game, but the foundations are solid and interconnected. Every new rule or mechanic ripples through the system in a way that makes the design feel alive.

---

### Looking Back

AI didn’t design this game. But it helped me test ideas faster, spot flaws earlier, and push through creative blocks.

What surprised me most wasn’t the cleverness of any single AI output. It was how much momentum I got from the **dialogue itself**. The interaction between my intent and the AI’s output was where the creativity lived.

I started this whole thing chasing a nostalgic itch for a half-forgotten 90s RTS. I ended up building the foundations of a brand new board game.

And I don’t think I would have got there without treating the AI as a collaborator.
