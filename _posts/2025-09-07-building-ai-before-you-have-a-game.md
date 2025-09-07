---
layout: post
title: "Building AI Before Building the Game: A Cautionary Tale"
date: 2025-09-07 11:00:00 +0000
categories: personal python board-game
---

_The curious case of Sky Islands and the Endless Roads leading nowhere ...._

---

### Lost in the Sky Islands: My First Attempt at AI for a Board Game

![When Agentic programs go wrong](/assets/agentic_gone_wrong.png)

I’ve been on a mission to design a board game — [*Sky Islands*](https://vanonselenp.github.io/2025/08/21/sky-islands/) — and build a simulation of it in Pygame so I can playtest it digitally.

As a seasoned engineer with 14+ years of experience, you’d think I’d take a well-organized, disciplined approach to building my game: a clear Trello board, carefully prioritized tasks, and a smooth, methodical path from prototype to polish.

Except… no.

Instead, I’ve been wandering from random idea to random idea, in a meandering creative hike with zero map and no water bottle.

Lately, I’ve been closing in on a pretty complete rules implementation: combat is figured out, island control works, magic buffs and damage systems are in place, and the Pygame simulation is *almost* bug-free.

Which naturally meant it was the **perfect time** to… add AI.

---

### Enter the LLM AI Player

Traditional game AI is this slow, careful, deeply technical craft. It takes months — sometimes years — to tune and polish.

So in my infinite wisdom, I skipped all that and said: *“Nah. Let’s just use an LLM as the AI.”*

Better yet, let’s make it **fully agentic**. Surely if I give it a prompt and some game state data, it’ll play like a pro.

Here’s part of what I gave it:

```
You are an AI player in Sky Islands, a strategic card game. 
You control {self.faction_name} with {self.strategy_name} strategy.

Core principles:
- Maintain resource economy
- Protect your base
- Control valuable islands
- Use command points efficiently

Always respond in this exact format:
ACTION: [action_name]
TARGET: [target_if_needed]
REASONING: [brief explanation]

CRITICAL: Only use actions from the "AVAILABLE ACTIONS" section.
```

It seemed foolproof.
Even better, I didn’t have to pay for every token — I hooked the OpenAI API up to a local LLM and got free AI gameplay. Perfect, right?

---

### The Dream… and the Reality

The AI did **exactly one thing well**: write extremely *convincing* reasoning for its moves.

Like this:

> "I'll acquire the Roads island to improve connectivity and expand my territory, while also gaining a foothold on the board. Since it's a low-cost island and cannot have generators built, it won't disrupt my resource economy. This action will also give me more options for future expansion and defense."

Sounds smart, right? A master strategist!

![road to nowhere](/assets/road_to_nowhere.png)

Except in practice, it did this for 20 turns straight — acquiring road after road, until it had a glorious chain of roads leading absolutely nowhere.

My digital empire was basically a medieval fantasy version of the UK’s motorway network.

Turns out, **getting AI to work right is hard**. Who knew?

---

### What Went Wrong

I had made two big mistakes:

1. **No actual game tools.**
   I was giving the AI text descriptions and asking it to pick actions, but it had no real way to *interact* with the game world. I should have built proper [MCP](https://modelcontextprotocol.io/) tools so the AI could *act*, not just talk.

2. **Building before understanding.**
   I jumped into AI development before I had a clear idea of what I was even making. It was scope creep disguised as “innovation.”

Basically, I was trying to build a self-driving car while still figuring out how to assemble a bicycle.

---

### Takeaways

1. **If you’re going agentic, build tools first.**
   Don’t just toss prompts at an LLM and hope for intelligence. Give it structured ways to interact with the game world.

2. **Figure out what you’re building before adding AI.**
   AI shouldn’t be a replacement for clarity — it should come after you understand the game design itself.

For now, my AI dreams are on pause. Back to the basics: fixing my Pygame simulation and actually finishing the game rules.

Because the real Sky Islands challenge wasn’t the enemy factions, or the balance issues, or even the road spam.

It was me.
