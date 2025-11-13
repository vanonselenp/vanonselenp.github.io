---
layout: post
title: "How to Get Things Done When You Have Nothing but Process"
date: 2025-11-13 08:00:00 +0000
categories: godot vibecoding claudecode specdrivendevelopment
---

_The tale of how a good System can carry you through the dark times..._

---

![banner](/assets/no-energy-week/banner.png)

This week I had zero motivation. Motivation tank completely empty.

My goal was 4 creatures and all of the remaining abilities. I only manage to build 2 creatures and 7 abilities instead.

That happening was astonishing to me.

But it did. And the reason isn't hard work or willpower, it's process. The structure on how to work with AI that I follow is robust enough to produce good work even when I have nothing left. That's the real story.

## How the structure holds up

My process is straightforward: compact the conversation, use the spec to guide the next iteration, verify the implementation, have the AI explain what it did, then manually test each ability. Rinse and repeat.

The spec-driven approach kept context alive, for me *and* the AI. While my motivation was completely drained, the AI kept building. I basically did the bare minimum each day before switching to Marvel Spider-Man, but the structure meant I never lost the thread. I was running on [Seinfeld method](https://www.youtube.com/shorts/mVQ1bzd816I) momentum: just keep the chain unbroken.

But here's the critical bit: **verify everything the AI makes**. The AI will confidently insist "Everything works perfectly!" and update your docs without being asked. Then you test it. Nothing works. You point it out and it turns out half the feature wasn't there to start with. Point it out again, and more unfinished work is found. The AI is capable and also will miss the obvious. Trust but verify.

**Pro tip**: never ever let the AI update the docs without being directly asked to.

This verification habit isn't just bug-catching. It is the key habit that keeps the process from collapsing. Without it, you're just building on sand. With it, even a low-energy week produces solid work.

## Where designs actually get good

The most valuable phase in my workflow is when the AI explains what it just built. That's where I stop and think: does this ability actually do what I want? Should it shift? Should it do something different?

That's where the magic happens.

![tank](/assets/no-energy-week/tank.png)

The Biomass Tank's parasitic bond is a perfect example. It started as a triggered ability, shifted into an activated passive that heals the Tank whenever *any* nearby enemy creature takes damage. That single design decision cascaded: upkeep suddenly mattered. Rounds had weight. Generator buildings became far more valuable, and vunerable. The creature went from decent to a potential powerhouse with two different healing methods and the ability to stay safe at range.

The design got better not because I worked harder on it, but because I paused to think about what it *was* and what it *could be*.

![defender](/assets/no-energy-week/defender.png)

Same with the Voltage Defender. Its pull mechanic started simple—nudging creatures around the battlefield. But when I stopped to think about it, it shifted: what if it could move creatures *off islands entirely*? Suddenly it's a broad control tool, shutting down buildings and repositioning the entire battlefield. That cascaded too—every ability needed rework. The EMP got bigger, affected every building including the player's, made positioning critical.

This reflection loop, building something, stopping to think about it and then nudging the design. It keeps creating moments where the game gets better. It's where iteration actually matters.

## The real lesson

Turns out the structure matters more than the fuel. Low-energy weeks aren't failures. They're tests of process.

When you have nothing left, you find out what actually works. This week proved that good structure, spec-driven development, verification habits, and the discipline to reflect, can carry you through. The creatures got better not because I pushed harder, but because the process was solid enough to ship good work anyway.

I might not have had the energy. But the system did.

Next week, fingers crossed, I will hopefully be finished the creature cards and start working on spells like Meteor and Lightning and getting some more buildings working correctly.