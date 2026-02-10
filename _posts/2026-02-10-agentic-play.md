---
layout: post
title: "This Is the Way: Delete the Code"
date: 2026-02-10 08:00:00 +0000
categories: vibecoding claudecode specdrivendevelopment codex
---

_How I learned to do AI Katas and make disposable code helped me recover from burnout_

---

Burnout is real, and it takes time to work its way out.

I spent the last couple of months trying to work up the will to tackle game projects again. Every attempt fizzled. After a 3+ month slog on a project that [refused to reach an end state](https://www.petervanonselen.com/2025/11/20/scope-creep/). I had nothing left.

So instead of committing to another massive project, I started playing.

I came across the Ralph Wingum loop ([30-min video if you're curious](https://www.youtube.com/watch?v=RpvQH0r0ecM)) and decided to experiment. The premise is simple: use two Claude skills and a bash script to let an AI go full agent mode. The first skill, `/prd`, takes a spec and generates user stories with verifiable acceptance criteria. The second, `/ralph`, converts that PRD into JSON. Then you loop over the JSON until done. This is basic agentic coding, but AI-agnostic and surprisingly effective.

![the wiggam loop](/assets/agentic-play/image.png)

I needed a project to test this on, so I picked [V-Sabotage](https://boardgamegeek.com/boardgame/163474/v-sabotage). It's a board game I enjoy but rarely get to play (toddler life), and more importantly, it's simple enough to define a clear MVP: rooms, a player, guards, sneaking mechanics, a win condition. I'd learned my lesson about scope.

The real experiment wasn't building the game. That was just the head fake. It actually was figuring out how to break down the work. How big should each PRD be? Do you treat each milestone as its own PRD? Do you throw the whole spec at it and see what happens?

I had to find out.

**First run:** I threw a PRD at the skills, ralphed it, and looped on a fresh repo. What came out was very familiar from the last time I was building a game in Godot with AI. Bascially something that worked, but buggy, clunky, no tests, poor signal architecture, tightly coupled code.

**Second run:** Same PRD, same loop, but this time I initialised the repo with a CLAUDE.md file first. Just basics: test-drive the code, use Godot 4.x best practices, that sort of thing.

The difference was dramatic. The AI wrote its own test runner. It test-drove everything, achieved high coverage, produced cleaner interfaces, used signals properly, and kept things decoupled. Twenty minutes of compute, and the output was genuinely good. Honestly the thing that blew my mind on this was __it wrote it's own TEST RUNNER!?!?__. Are you kidding me?

So ... key lesson: agent files matter. A lot.

**Third run:** I embedded full milestones into the PRDs—a dozen user stories each, multiple acceptance criteria. The loop churned through it and produced a testable MVP in surprisingly little time.

![stealth game](/assets/agentic-play/tactics.png)

**Fourth run:** I got distracted by an app idea. Spent a couple of hours refining it with AI, generated a chunky PRD, threw the whole thing at the `/prd` skill. It produced 40 stories. I looped it. An hour later, with 5% of my usage allowance remaining, I had a working prototype.

![random app](/assets/agentic-play/mobile-app.png)

It didn't do exactly what I wanted. But it did most of what I'd asked. This was surprisingly more than enough to immediately change my thinking about what I actually needed in a meaningful way. 

And here's the thing that made all of this feel like play instead of work: **I deleted the code.**. I went full [code retreat conways game of life](https://www.coderetreat.org/) delete the code. 

Multiple times. Deliberately. The output I was chasing wasn't a codebase. It was understanding. How big can a PRD get before the loop breaks? (Bigger than I expected.) How much do agent files matter? (More than I expected.) What's the minimum setup to get something useful? (Less than I expected.)

Disposable code meant low stakes. Low stakes meant I could experiment freely. And experimenting freely, it turns out, is how I recover from burnout.

This play has fundamentally changed how I work at The Economist. But that's a story for next time.