---
layout: post
title: "Why You Shouldn't Speedrun a Production Refactor"
date: 2025-12-12 08:00:00 +0000
categories: godot vibecoding claudecode specdrivendevelopment
---

_Learning the hard way that AI makes discipline more important, not less..._

---

This week has been a mess. I've been ill since last Thursday with a cough that's been both productive and dizzying, which in a rare moment of clarity made me realize that maybe doing personal dev in the evenings is... not ideal. So no game dev tales this week. 

Instead, I want to talk about how I nearly torpedoed a production refactor at The Economist a month ago by forgetting the most important lesson I've been learning over the past few months: **AI makes discipline more important, not less.**

## The spectacular failure

I'm currently on the e-comm-funnel team working on the checkout pipeline. One of my first projects has been tackling Commerce Services. This is a Go monolith (a language I'd never used before recently) that started as a POC and got productionized. Naturally, it's a beautiful mess with conflicting APIs doing all sorts of non-cohesive domain things.

My goal: break it into microservices.

So naturally I did what I've been practicing with Horizons Edge and started with a spec. I had a very long conversation with Codex, analyzed the repo structure, identified the domains, mapped dependencies. From this chat we produced a solid 10 page high-level plan. 

And the first step of that plan was _Phase 1: extract common code into a shared library_.

And somewhat predictably, here's where I got clever.

I thought: "I've got a detailed spec. Codex knows Go. Let's just... do the whole thing! Whats the worst that could happen?"

So I did. One massive refactor. Codex happily obliged.

Then I looked at the pull request: **200 files changed in the monolith. 80 files in the new library.**

![this is fine, right?](/assets/speedrun-refactor/this-is-fine.png)

And I just stared at it, completely overwhelmed by the obvious question: *How the hell am I going to verify this actually works?*

There was no way I could meaningfully review 280 files of changes. No way I could ask another engineer to do it. No way to be confident this wouldn't break something subtle in production. I'd just created an unshippable monster.

## Starting over, properly this time

I scrapped the entire thing and started again with an "I need this to be incremental" mindset.

Not just because I wanted to be able to review it, though that's critical, but because I genuinely believe small releases into production are the right way to work. It should have been my default starting point. Instead, I'm still learning just how disciplined I need to be when working with AI tooling.

The new approach:

**First**, I wrote a much more detailed spec for Phase 1 that lived in the new repo. Not just "extract shared library" but an 8-step plan where each step could go to production independently. Start with the absolute minimum: just one joint service with no dependencies. This would validate the CI/CD pipeline, the integration points, everything, with the smallest possible change.

**Then**, one step at a time:
- Extracted and deploy leaf utilities (logging, validation, middleware)
- Migrated HTTP routing abstractions
- Moved observability and AWS helpers
- Extracted infrastructure components like health checks
- Finally, the component registry

At each step: tested, improved coverage, deployed to production, monitored. The existing systems kept running exactly as before.

I followed the same hyper-methodical approach I've been using with the game project. Focusing on small scoped MVP slices and incremental delivery. For the actual development, I loaded Codex into a workspace with both repos and had it follow the spec file for each migration. Then validated with Claude in GitHub Copilot, extensive personal review, and eventually team review before each production deployment.

The result: A refactor of a core system touching ~200 files, in a programming language I'm just learning, in a domain I'd just joined, completed over a couple of weeks with zero downtime. No one on the team was blocked or impacted. It just happened quietly in the background.

## What I'm taking away

Two things keep reinforcing themselves across contexts:

**First**: AI amplifies your need for discipline. The easier it becomes to generate large amounts of code, the more critical it is to think carefully about scope, verification, and deployment strategy. One-shotting 280 files feels productive in the moment. It's not. It's just creating an unshippable mess you'll have to undo.

**Second**: The "what's the smallest increment that adds value?" mindset pays off everywhere. It saved Horizons Edge when I was drowning in scope creep. It made this refactor safe and reviewable. It's not just a nice-to-have for side projects ... it's how you de-risk production changes in unfamiliar territory.

Next up is breaking out actual domains into microservices, starting with Identity & User. But that's a plan for next year, when I'm hopefully no longer coughing my lungs out.