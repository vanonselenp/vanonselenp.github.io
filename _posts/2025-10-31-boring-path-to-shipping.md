---
layout: post
title: "The Boring Path to Actually Shipping with AI"
date: 2025-10-31 08:00:00 +0000
categories: personal godot video-game claudecode vibecoding
---

_Or: How I Learned to Stop Vibing and Love the Spec"_

---

OMG. This [spec driven development](https://www.petervanonselen.com/2025/10/30/exert-of-what-i-learnt/) process is BORING!

Okay okay, for reals though, following this process of using a spec and a clear breakdown of tasks is tangibly yielding results and making remarkable progress forward in the game.

![3 heroes](/assets/boring/3-heroes.png)

**In the past week I have:**
- Created 3 new creatures: one that moves fast, hits hard and stuns enemies; another that spawns minions and multiplies when it dies; and one that shoots a bolt that blows things up and destroys land all over the place
- Around 9 new abilities created and working
- Got the AI to hack some terrible models together so they would be unique enough to be playable
- Made the islands generate more interestingly
- Completed a horde of UI cleanups
- Handled some general refactorings and got a bunch of systems working
- **Total changes:** 52 files modified, +3,718 lines, -474 lines across 34 commits all for about 10 hours effort.

By basically all metrics... productive?

## So Where Did the "Boring" Comment Come From?

It comes down to what following the spec driven development process has actually become. Now that I'm being militant about making AI follow a todo list, what I've functionally done is put on multiple hats:

**Product Manager hat:** Created a complete game design doc. High-level, aspirational, covering combat systems, creatures, abilities, victory conditions — the whole vision thing.

**Delivery/Feature Lead hat:** Took one section (the combat system) and broke it down into actual features. Not just "build combat" but "what does combat *need*? Movement? Attacks? Status effects? Death?" The unglamorous work of turning vibes into verbs.

**3 Amigos hat:** Turned those features into a massive todo task list. Every checkbox a micro-commitment. "Add blink ability." "Implement stun on hit." "Make multiplying enemy spawn minions." The kind of granular breakdown that makes you feel like you're doing corporate sprint planning for your hobby project.

**Engineer hat:** Actioning the tasks one at a time. No wandering off to make prettier models. No "oh but what if the islands had weather systems?" Just: checkbox, code, commit, next checkbox.

**QA hat:** Testing behavior. Does the stun actually stun? Does the explosion destroy terrain properly? Do the spawned minions inherit the right stats? The tedious-but-essential validation loop.

**The realization:** I've become .... an entire agile team.

And what that practically means is that I've made gamedev into *work*. My day job. God damn it.

Spent a lifetime developing habits on how to do engineering, and then you get a newfangled tool and you just... follow the process. Good job me. Yay! Right? ...Right?!

## The Tangents I Didn't Follow (And Why That Hurts a Little)

I'll be honest: getting lost in tangents and running away with the vibes is a whole hell of a lot of fun.

In past weeks, I would have absolutely gone off on any of these:

**Visual polish:** Using all the gorgeous tiles from Kenney's asset packs to make everything look beautiful instead of just functional. Making each creature feel distinct and characterful instead of "placeholder cube with stats."

**Procedural generation rabbit hole:** Diving deeper into Wave Function Collapse algorithms to generate more dynamic, interesting terrain. Making islands that feel hand-crafted even though they're algorithmic.

**Creature personality:** Actually modeling unique designs for each bot. Giving them visual identity, animations, character beyond their mechanical function.

**Worldbuilding:** Fleshing out the lore of the different factions. Their motivations, their aesthetics, their place in this weird sky-island world I'm building.

These are the *fun* parts. The parts where you lose track of time because you're following curiosity instead of a checklist. The parts that make gamedev feel like *play* instead of *work*.

But here's the thing: **none of them get me closer to a playable game.**

They're all polish on a foundation that doesn't exist yet. They're the dessert when I haven't finished the vegetables. So the spec says: not now. Stay focused. Ship the MVP first.

It's the right call. I know it's the right call. Oh heavens please let this be the right call ...

And I hate how boring the right call is.

## The Discipline vs. Fun Paradox

Being strictly disciplined with myself about how to dev with this tool is *super productive*. Lots of forward momentum in an actual direction is really fantastic.

And also... boring.

There's something deeply satisfying about seeing the commit graph fill up. About checking off todo items. About watching the line count grow in a structured, intentional way. It feels *professional*. It feels like I'm actually building something instead of just playing around.

But it's missing that chaotic energy that made the early weeks of this project so intoxicating. The "what if I just try this wild thing?" moments. The tangents that turned into features I didn't know I needed.

The spec process works. It's just not romantic.

## Where I'm Headed

My plan is to stay disciplined until I hit what I'm calling an "exit point" — a milestone where the game is functioning *just enough* to validate the gameplay and experience. Right now, that means:

- **2 unique decks** that feel different to play
- **Basic strategy cards** that offer meaningful choices
- **Fog of war** (because exploration matters in a tactics game)
- **A simple victory condition**

It won't be *done*. But it will be **playable**. And **testable**. A real artifact I can put in front of someone and ask: "Is this fun?"

Following this process is giving me something I've never had before in side projects: **predictable, consistent progress**.

Not explosive bursts of inspiration followed by month-long abandonments. Not chasing vibes until I hit a wall and lose interest. Not 10,000-line notebooks that collapse under their own weight.

Actual, measurable forward motion toward a concrete goal.

![current](/assets/boring/chaos.png)

## The Bottom Line

Is it boring? Yes.

Is it working? Also yes.

And maybe that's the trade I need to make right now. There's a time for tangents and vibes — I spent weeks in that mode and learned a ton. But there's also a time to put your head down, follow the checklist, and *actually finish something*.

The irony isn't lost on me: I spent four months learning how to use AI as a collaborator, only to discover that the real unlock was bringing back all the boring engineering discipline I use at my day job.

Turns out "vibe coding" still requires structure. Who knew?

Next week: More abilities. More discipline. More checkboxes. And hopefully, one step closer to knowing if this game is worth making at all.

---

**P.S.** If you're following along with this devlog and thinking "wow, this sounds like he's sucked all the joy out of his hobby" — yeah, a little bit. But also: I'm actually *building* something now instead of just dreaming about it. So maybe boring is the price of shipping.

We'll see how I feel when I hit that exit point.