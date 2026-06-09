---
layout: page
title: Projects
permalink: /projects/
description: A short, honest list of the things I have built. Tools you can clone, and builds with a story attached.
---

Two halves. The tools are small repos you can clone and use. The builds are bigger things I have been making, each with a thread of posts behind it.

## Tools

### harness-bench

[github.com/vanonselenp/harness-bench](https://github.com/vanonselenp/harness-bench)

A rig for comparing AI coding harnesses against each other. Same prompt, same starting state, every harness and model combination, multiple runs each, all graded against a hidden Vitest suite the agent never sees. The point is to stop arguing about which harness is best from vibes and actually grade them, then look at the results and argue from those instead.

**Related reading:** [Show Your Work](/2026/05/06/show-your-work/)

### print-bench (`pb`)

[github.com/vanonselenp/print-bench](https://github.com/vanonselenp/print-bench)

A Python CLI for the concept-to-3D-print workflow I use for tabletop miniatures. A filesystem with opinions, a CLI with verbs. `style.md` for the things that stay stable across an army, `subjects.yaml` for the things that vary, `seed.png` for the visual anchor. Then a tiny set of commands to assemble the prompt, crop the front and back views, push them to Meshy, and fetch the model when it is ready. Deliberately contains no AI. The AI work happens in the chat windows it shepherds you between.

**Related reading:** [The Best Part Has No AI in It](/2026/05/18/best-part-has-no-ai-in-it/)

### zsh wrapper functions

[github.com/vanonselenp/zsh-functions](https://github.com/vanonselenp/zsh-functions)

Small portable wrappers around the harnesses I actually use. The reason they live in zsh instead of a harness plugin is that my workflow needs to survive across Claude Code, OpenCode and Codex, and tying it to any one of their plugin systems is how you end up rewriting everything the next time the wind shifts.

**Related reading:** [The Grand Plugin Trap](/2026/04/11/the-grand-plugin-trap/)

### agentic-katas

[github.com/vanonselenp/agentic-katas](https://github.com/vanonselenp/agentic-katas)

A set of code-retreat-style exercises for practising agentic coding with another person. Each kata is a deliberately ambiguous brief with a privacy constraint and an extra-credit extension. The rule that does the work: you are not allowed to pick a language or framework until you have had a real conversation with the agent about the approach. The thing you build does not matter, the process does.

## Builds

### Horizon's Edge

![Horizon's Edge splash](/assets/splash.png)

[github.com/vanonselenp/horizons-edge](https://github.com/vanonselenp/horizons-edge)

A tactical wargame in Godot. Floating islands, hex grid, height-based combat, card-driven actions, procedurally generated maps using Wave Function Collapse. It began as a sensible cardboard prototype and immediately grew legs, then a digital version, then a combat system, then a road network, then several refactors I could probably have skipped. It is the thing I work on when I want to find out whether an AI-assisted process can carry a real project through the messy middle, not just the impressive opening.

**Toolchain:** Godot, GDScript

**Related reading:**
- [Sky Islands](/2025/08/21/sky-islands/)
- [I Just Wanted to Make a Board Game and Now There Are Procedural Islands](/2025/09/07/boardgame-to-digital/)
- [Road to Combat Paved with Blink](/2025/10/17/road-to-combat-paved-with-blink/)
- [From AI Skeptic to Constant Collaborator](/2025/10/20/what-i-have-learnt/)

### Bolt Action 3D print pipeline

![Soviet army for Bolt Action](/assets/army-of-prompts/hero.jpg)

A side project that turned into a process experiment. A chain of generative tools going from a concept image to a printable miniature for the tabletop wargame Bolt Action. ChatGPT for concept work, then a 3D model generator, then Bambu Studio to slice, then a printer to make the thing real. Two 1000-point armies so far, around fifty unique sculpts each, all scaled down so they actually fit on a kitchen table.

The 3D step started as just Meshy, because Meshy was good enough and good enough is a powerful drug. It now sits behind an adapter so I can swap between Meshy and the Replicate-hosted alternatives (hyper3d/rodin, several Hunyuan variants, Trellis) without rewriting the workflow each time one of them improves.

**Toolchain:** ChatGPT (concepts), Meshy and Replicate (image-to-3D, via an adapter covering hyper3d/rodin, Hunyuan variants and Trellis), Bambu Studio (slicing), Bambu printer (FDM). The plumbing for all of this lives in [print-bench](#print-bench-pb).

**Related reading:**
- [I Built This In A Prompt Window! With A Box Of Filament!](/2026/04/22/vibe-coding-reality/)
- [An Army of One Prompt](/2026/05/10/an-army-of-one-prompt/)
- [Doesn't Look Like Anything to Me](/2026/05/27/doesnt-look-like-anything-to-me/)

### MTG Jumpstart Cube Constructor

![Magic splash](/assets/magic-splash.png)

The project that started this whole arc. A Python tool that builds themed Magic: The Gathering Jumpstart cubes from an arbitrary card pool, with theme extraction and per-archetype scorers doing the heavy lifting. I built it because I wanted a cube and did not want to hand-curate one, and somewhere in the middle of it I realised I was working with the AI differently than I had before. Most of what I have written since traces back to that.

[github.com/vanonselenp/magic-jumpstart](https://github.com/vanonselenp/magic-jumpstart), with a [live cube on Cube Cobra](https://cubecobra.com/cube/list/pauper-jumpstart-06-2025).

**Related reading:**
- [Jumpstart Cube Catastrophication](/2025/08/04/jumpstart-cube-catastrophication/)
- [From AI Skeptic to Constant Collaborator](/2025/10/20/what-i-have-learnt/)
