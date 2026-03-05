---
layout: post
title: "How I Learnt to Stop Worrying and Love Agentic Katas"
date: 2026-03-05 08:00:00 +0000
categories: claudecode specdrivendevelopment katas softwarecraftsmanship
---

_I don't know how to teach this. But I think I've figured out how to practice it..._

---

Have you ever struggled to get started with something new—not because the thing itself is hard, but because the *shape* of how to learn it isn't clear? That's where I've been stuck with agentic coding. Not the doing of it. I've been doing it for months. The teaching of it. The "how do I help someone else get started" of it.

And then I remembered code retreats. And katas. And the way I actually learned TDD all those years ago—not from a book, but from structured practice with low stakes and room to play.

So I built a set of agentic katas: structured coding exercises designed specifically for practising AI-assisted development. Not traditional katas—those are too small and the AI already knows all the answers. These are bigger, meatier problems in unfamiliar domains that force you to engage with the full process of working alongside an agent.

Let me explain how I got here.

## A Brief History of Practising on Purpose

Early in my career, code retreats were the thing that taught me test-driven development. Not a book. Not a course. A structured, all-day event where you solve Conway's Game of Life over and over again, each time with different constraints. Maybe your pair is actively trying to *not* solve the problem. Maybe you're strictly ping-ponging. Maybe you delete your code every 45 minutes.

The point was never to solve Conway's Game of Life. The point was to internalise the patterns and practices of TDD by giving yourself a safe space to experiment. No production pressure. No deadlines. Just play.

Code katas grew out of the same ethos—small, self-contained problems that shouldn't take more than an hour or two. The algorithm doesn't matter. How you choose to solve it does. They're bite-sized by design. They're not supposed to be hard. They're supposed to be *practice*.

## The Problem with Katas and AI

Here's the thing I've been struggling with: traditional code katas don't work for learning agentic development. They're too small. The LLM has already seen every solution to FizzBuzz and Roman Numerals in its training data. You're not practising a workflow—you're watching an AI regurgitate a known answer. There's nothing to explore, nothing to plan, no decisions to make about approach or tooling.

And that matters, because the skill you need to develop with agentic coding isn't "how to prompt an AI to write code." It's how to *think alongside one*. How to explore a problem space together. How to write a plan that gives an agent enough context to be useful. How to verify that what came back is actually what you wanted. How to set up your workspace so the AI has the right guardrails.

None of that shows up in a 30-minute kata where the AI already knows the answer.

## The Accidental Discovery

What's funny is that I've kind of been doing agentic katas already—almost by accident. I just didn't realise it at the time.

![The first kata](/assets/agentic-kata/kata1.png)

A few weeks ago I wrote about [deleting code on purpose as a way to recover from burnout](https://www.petervanonselen.com/2026/02/10/agentic-play/). I'd been experimenting with the Ralph Wingum loop—throwing PRDs at an agentic coding workflow, seeing what came out, then deliberately throwing the code away. The output I was chasing wasn't a codebase. It was understanding. How big can a PRD get before the loop breaks? How much do agent files matter? What's the minimum setup to get something useful?

Each run was a contained experiment. Fresh repo, clear problem, focused practice, delete the code, do it again. I was varying one thing at a time—adding a CLAUDE.md file, scaling up the PRD size, trying a different domain—and learning from each iteration.

I was doing agentic katas. I just hadn't named them yet.

Looking back, the whole arc has been building toward this. My game project was the first rough version—months of cycling through spec-driven development and making mistakes. The "delete the code" experiments compressed that into focused sessions. And now, formalising the structure into something other people can pick up feels like the obvious next step.

## Building the Thing

So I've put together a set of agentic katas. The idea is that each one should require somewhere in the region of four to eight hours of focused hand crafted work to do *well*. And by "well" I mean the full golden plate: test-driven, 100% coverage, clean README, proper git history, the works. Not because the output matters—but because doing that level of work with an AI agent forces you to actually engage with the process.

The loop for every kata is the same:

**Explore** → **Plan** → **Set Up Context** → **Build** → **Verify**

And there's one key rule that makes the whole thing work: *you are not allowed to choose a programming language or framework until you've had a conversation with your AI tool about what the best approach is.*

This is the rule that forces the shift. Instead of jumping straight to "build me X in TypeScript," you have to start with "I need to solve this problem—what are my options?" You explore the problem space. You figure out what tools exist. You have the AI challenge your assumptions. *Then* you decide on an approach.

From there, you write a detailed plan—acceptance criteria, example data, use cases, a breakdown into small chunks of work. You set up your workspace with an agent file and think about what context to include. You build incrementally. And you verify everything: read the plan, read the code, run it, test it, confirm it does what you intended.

![the loop](/assets/agentic-kata/agentic-kata-loop.svg)

## The Katas Themselves

I've started with four problems, each chosen because they sit in a domain most developers haven't worked in before:

An **audio transcriber** that handles speech-to-text with timestamps and speaker diarisation. A **background remover** for image segmentation. A **meme generator** that deals with text rendering and positioning on arbitrary images. And a **thumbnail ranker** that scores images for visual appeal.

Each kata has deliberate ambiguity baked in—because real problems are ambiguous, and part of the skill is figuring out what questions to ask. They also have a privacy constraint (everything runs locally, no cloud APIs for processing) and an extra credit extension for when you want to push further.

## Why This Matters Right Now

I'll be honest: the reason I'm putting this together is partly selfish. I want to run a workshop with my colleagues, and I need structured material to do it. But there's a bigger motivation too.

Right now, everything about AI and software development feels incredibly intense. Fear of being made obsolete. AI layoff discourse everywhere. The pressure to have strong opinions about tools you've barely had time to evaluate. It's all very stressful, and stress is the enemy of learning.

What people actually need—what *I* needed, and what I accidentally created for myself—is a safe space to play. A contained environment where you can try things, make mistakes, and build intuition without the stakes of production code or career anxiety hanging over you.

Code retreats gave us that for TDD. I'm hoping agentic katas can do the same for working with AI.

## The Repo

I've put everything together in a repo: [github.com/vanonselenp/agentic-katas](https://github.com/vanonselenp/agentic-katas)

It includes the kata briefs, a participant guide covering the rules and process, and a facilitator guide for anyone who wants to run this as a structured session with their team. A session takes about 90 minutes.

I haven't run this with anyone else yet. I only put it together today, and I'm planning to trial it with my team in the coming weeks. It might be brilliant. It might be terrible. Either way, I'll write about how it goes.

But the core idea—that you need bigger, unfamiliar problems to practise AI-assisted development, and that the process matters more than the output—that I'm confident about. Because I've been living it, accidentally, for months.

If you try it, I'd love to hear how it goes. And if you're doing something different to build these skills, I'd love to hear about that too.