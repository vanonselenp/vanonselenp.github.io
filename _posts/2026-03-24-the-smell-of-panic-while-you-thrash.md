---
layout: post
title: "The Smell of Panic When You Context Thrash"
date: 2026-03-24 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_High high hope for the code, shooting for a PR when I couldn't even make a commit..._

---

![Panic at the keyboard](/assets/panic.png)

Over the past few weeks I have been increasingly panicked. That's probably the only honest way to frame it.

I've been juggling a lot. Supporting a team building out a new payment method. Handing over deep knowledge of an existing payment method to another team working outside our scope but integrating with systems we own. Helping yet another team figure out how to break a backend platform service from a monolith into microservices. And somewhere in between all of that, trying to actually deliver a feature myself: a seemingly straightforward change to one of our frontend purchase journeys to make it faster.

Each of those things individually requires serious context. Together they've been chewing up my headspace and pulling me in every direction. Which means that whenever I finally sat down to write actual code, I arrived in a state of absolute panic. The "oh my gosh I have so little time, move quickly, move quickly, move quickly" kind of survival mode.

And that's when I made one of the most fundamental mistakes you can make with AI-assisted development.

## The 50-File Disaster

Here's the thing about AI-generated code: it's easy. So easy that it's almost impossible to remember just how easy it is, because you've spent a lifetime handcrafting code yourself. You carry this default assumption that building things is complicated and slow.

So I did what I thought was the right thing. I planned. I looked through the existing code. I thought about it. I wrote out detailed acceptance criteria. I thought about the problem from the AI's perspective. And then I said "cool, I think I have enough" and started implementing.

By the time I got someone else to look at it, they pointed out it was missing a key behaviour. I'd misunderstood part of the acceptance criteria. OK, fine. I started trying to fix it.

And then trying to fix it. And trying to fix it.

What was a small hole became a deep hole became a nightmare became "why does it feel like I will never, ever get anywhere with this?" By the end of it I was touching something like 50 files across two repos. Small changes scattered everywhere, most of them not even really needed. All driven by the panic override of needing to get something done while constantly being pulled out of context and back in and out and back in until I was just thrashing. Burning cycles. Making zero progress.

## Panic Is a Smell

If you've been in software long enough you know what a code smell is. Something that isn't technically broken but tells you something deeper is wrong.

The panic to get things done is a smell. The pushing and pushing and pushing is a smell. The feeling that you don't have enough time, that you have to ship something right now, that you can't afford to slow down? That's a smell. And I ignored it for way too long.

Because here's the lesson I apparently need to keep re-learning: with AI-assisted development, *the writing of code is not the bottleneck*. It never was. The understanding is the bottleneck. And when you're panicking, you skip the understanding to get to the doing, which is exactly backwards.

## The Reset

I eventually stopped. Stepped away from the mess. Started with a brand new repository. Took all the things I'd learned, the plan document, the acceptance criteria, everything. And then I spent an entire day in conversation with an AI. Not writing code. Just investigating.

Testing existing behaviour. Running multiple examples and execution paths. Making sure I had a precise, clear understanding of what the current system actually did, what the new behaviour needed to be, and all the various paths between them. I literally spent hours asking the AI to explain each step of its plan and justify why it chose that approach.

I say all the time that planning matters more than coding. But experiencing the contrast firsthand is different. Hours of slow, methodical, back-and-forth investigation. Deep thinking about context. Deep thinking about what you're trying to do and why. So that when you, *the human in the loop*, actually ask the AI to build something, the full context of what you're trying to achieve is sitting clearly in your head. You understand the user behaviour. The system interactions. The high-level architecture. You could draw all the diagrams because you actually understand what needs to be done.

The feature that had consumed a week and a half of thrashing? After that day of planning, it took a couple of hours to get something working correctly.

## The Council of AIs (or: Going Wide)

Meanwhile, on the other side of my work life, I've been doing something completely different with AI tooling.

To support the contracting team building out a new feature, I've been running what is essentially a council of AIs to review their design documents. OpenCode, Codex CLI, and Claude Code running simultaneously so I can verify, validate, and cross-compare. Deep-dive analysis with Claude and ChatGPT for architectural decisions and historical context. Complex investigation into bugs that were first logged two years ago and never properly resolved.

I have been holding the context of a massive amount of different workstreams. Work that would have taken me days or weeks to get even a baseline understanding of. The AI tooling genuinely lets you go wide in a way that wasn't possible before.

And that's where the tension lives.

## Shield and Sword

The honest truth is that I've been doing two very different jobs at the same time.

One job is the shield: absorbing context, running investigations, unblocking other teams, reviewing designs, holding the big picture so nobody else has to. The AI tooling makes this possible. It lets you hold 10x the context. You can pre-empt meetings by using Claude to pull together context and solve problems before the meeting even happens, cancelling two or three in a morning and buying yourself hours of uninterrupted time. You can run parallel investigations across multiple tools and hold the full picture of what's going on across an entire programme of work.

The other job is the sword: actually sitting down and delivering a piece of working software. And that requires the opposite of going wide. It requires going deep. Slow. Methodical. Boring, even.

The AI enables both.

But your brain can't do both at the same time.

When you try, you thrash. You burn cycles switching between deep and wide, and just like a thrashing computer, you end up doing a lot of work and making no progress.

## What I'm Taking Away

Two things, and they're in tension with each other, and I'm OK with that.

**Go deep before you go fast.** Planning with AI isn't just "write a spec and hand it over." It's hours of investigation. It's asking the AI to explain its own plan in painful detail. It's making sure you understand the problem so well you could solve it by hand. The code is the easy part. The understanding is the work.

**AI lets you hold a lot of context, but your brain still has limits.** Context switching costs the same as it always did. Maybe more, because the AI makes it tempting to take on everything. You can hold the shield and the sword, but not at the same time. Deliberately buying yourself blocks of deep time is not optional. It's the whole game.

This is the new trap for senior engineers. AI lets you take on more surface area than ever before. But the work that actually ships still requires deep focus. Nobody is immune to thrashing, no matter how good the tooling gets.

And if you're sitting there right now, pushing and pushing and panicking and feeling like you'll never get there? That's a smell. Stop. Step away. Start again with understanding, not urgency.