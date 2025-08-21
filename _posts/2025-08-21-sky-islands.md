---
layout: post
title: "Islands at War: Designing a Board Game with AI"
date: 2025-08-21 11:00:00 +0000
categories: personal python board-game
---

---

About two weeks ago I wrapped up a project that had completely consumed me: figuring out how to create a Jumpstart cube from a Pauper cube. For a few weeks it was all I thought about in my spare time — basically just spent every free moment vibing on it, even when I was watching a TV show with my wife. But while I was busy tweaking code to generate decks, extract themes, and balance relative deck strengths, another idea was quietly percolating in the back of my mind.

It started with a simple question: *do you remember NetStorm?*

![Netstorm in action!](/assets/netstorm.png)

For most people, the answer is no. It was a strange little RTS from the late 90s that barely anyone remembers today. But for me, it triggered an itch that just couldn’t be scratched — it’s impossible to play on modern tech without resorting to some dodgy site, but what if I could capture that vibe from a board game instead?

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

### The Island Game Takes Shape

The initial vision was a mashup:

* Magic: The Gathering’s **Jumpstart** randomness,
* Marvel Champions’ **card management**,
* and Star Wars: The Deckbuilding Game’s **capital ships** — except in my version, those ships were islands.

I started with a speculative chat that led to a rough design doc — high-level, but with enough of a skeleton to start iterating toward a solution. Then I followed it up with discussions about resource management, card flow, and how creatures might interact with the islands.

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
