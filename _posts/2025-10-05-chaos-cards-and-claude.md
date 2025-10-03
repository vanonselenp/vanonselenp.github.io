---
layout: post
title: "Cards, Chaos and the subtle art of Claude Code"
date: 2025-10-03 11:00:00 +0000
categories: personal board-game godot video-game claudecode codex vibecoding
---

_Last Time on Madness Boulevard..._

---

Last time on the wonderful adventures of a random walk down the boulevard of madness in making a ~~board~~ video game, I was busy refactoring cards and trying to get them to actually work.

![Cards Cards CARDS!](/assets/cards-chaos-claude/cards.png)

Now I have working CARDS! They discard! They look devy! They click! They discard! The UI is janky, but hey—it works. I’ve got… 3 cards. Three. OMG. Only 3 cards. \:mindblown: This is going to be harder than I thought (obviously).

## Factions of Madness

When I nudged Claude toward “cards instead of buttons” as a way to unify the gameplay, I immediately got ahead of myself. Naturally, I dreamed up two factions, a bit of lore, some shiny card concepts, and before I knew it… two half-baked 20-card decks *plus* a half-baked strategy deck. It was going to be over 9000!

The concepts were fun:

![Nezumi Swarm](/assets/cards-chaos-claude/nezumi.png)

**Nezumi Swarm:** Honorable rat samurai + endless undead swarm tactics. Weak but unstoppable. Multiplying and spawning more and more. For the SWARM!

![Aetheric Empire](/assets/cards-chaos-claude/aetheric.png)

**Aetheric Empire:** Victorian British Empire × Girl Genius mad science romance. Cyborgs, mechs, airship supremacy, love and madness.

The Romance. The Swarm. It was glorious.

## Overload Incoming

Then reality hit: instead of my usual TDD-style “one thing at a time, working confidently,” I was doing *everything, everywhere, all at once.* Unsurprisingly: overloaded. Cue the [“who’s on first, what’s on second, I don’t knows on third”](https://www.youtube.com/watch?v=sYOUFGfK4bU) situation.

So, the *logical* next step was to pause the chaos and implement turn/round structure. Makes sense, right? …Except instead I doubled back to cards. Because of course I did.

## Planning Docs, or Madness in Writing

Here’s the interesting part: working with Claude (and Codex) has led me to generate deep planning docs for features. I’ll spend hours iterating back and forth, treating them like living documents. Each doc builds context for the next, and since I’m writing them *inside* the codebase, they get deeply grounded in the actual work. It’s been a surprisingly useful feedback loop.

If you’re bored, you can peek at the [planning doc for Turn and Round Structure](/articles/horizons-edge/5-command-token-bag-system).  But spoiler: instead of building turns/rounds like a sane person, I realized maybe… just maybe… I should start small. Like, *test cards first.* Lego pieces before Royal Albert Hall.

Small steps. Right?

## Next Steps

So the plan now: get a test deck with basic cards sketched up and playable.

**Next steps: MORE CARDS!**

I’m focusing on functional requirements like:

* **Complete archetype coverage:** Territory, creatures, spells, interaction, combos
* **Energy-gated abilities:** Powers tied to energy types
* **Ability framework:** Up to 4 abilities per creature
* **Energy-scaling bonuses:** Special effects if fueled by the right energy

And covering these card types:

* ✅ Territorial Claim – Place core nodes
* ✅ Terraforming Push – Expand island
* ✅ Road Network – Connect islands
* ✅ Build Generator – Energy production
* ❌ Creatures with abilities
* ❌ Combat mechanics
* ❌ Opponent interaction
* ❌ Energy-specific bonuses

You’d think I’d take it easier this time, right? Nope. My card planning doc is 1,299 lines long. But this time, I’m getting Claude to implement *one card at a time.*

Let’s see how that goes.

Will I actually build a turn structure next time? Or just make *even more cards*? Until then, may your rats be honorable and your airships only slightly on fire.

Also, if you are counting, I am now up to using Claude Code, Claude, Codex, ChatGPT and Gemini to do this project ....