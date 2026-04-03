---
layout: post
title: "The Council Will See You Now..."
date: 2026-04-03 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_You were the chosen one! You were supposed to destroy the hallucinations, not join them!_

---

![The council](/assets/council/council.png)

I use multiple AI agents as an architectural review council. When I said that out loud recently, I got the look. You know the one. The polite nod that says "I have no idea what you just said but I'm going to smile and move on."

So here's the footnote.

## The setup

I'm currently juggling two things at work that have no business being juggled at the same time.

The first is a set of deeply tangled bugs that have been lurking since July 2024. They're tied to a third-party integration, they're interconnected, and we're only now seeing the full scope of how bad they are. This is slow, careful, multi-day investigation work. Long-form conversations with AI. Reading code. Writing tests to verify behaviour. Building the case for "this is exactly where the problem is and this is exactly why."

The second is supporting our engineering manager to enable an external contracting team to deliver a new feature in our codebase. The contractors have never touched our code before. They don't have a clear picture of the requirements, the systems, or how everything interacts. The depth they need to make meaningful architectural decisions is broad, deep, and nuanced. I've worked in the systems, but I don't have enough depth to answer all their questions off the top of my head.

But what I do have is access to Claude, Claude Code, GitHub Copilot, and Codex.

## The council, assembled

I should back up. For months now, in my personal life, I've been asking the same questions to ChatGPT, Gemini, and Claude interchangeably. I call them my council. Each one has a different personality, notices different things, and observes different angles. I find that when I'm getting multiple opinions I make better decisions. This is just me applying the same instinct to my workspace.

It started with a simple question: we have a third-party payment provider that offers a payment method, and we have a number of integrations between us and them. The contracting team needed to understand how we use it. How do we integrate with backend services? Where are the bits that are backend-for-frontend versus actual backend platform services? How do all of these systems interact? Where are all the endpoints?

I spent a day and a half in long-form conversations with multiple AI systems interrogating the problem. I started at the web-facing entry point and worked backwards. I trawled Confluence, Slack, Google Drive, and every other form of long-term documentation to build a picture of what the contracting team was going to need. Then I took all of that context, the goals of the team, and the documentation, and used it to structure a comprehensive prompt.

I ran that prompt through three different AI harnesses: Codex, Claude (via the web), and Claude Code running Opus. Each one went away, investigated the same repositories, and came back with structured answers. Then I took those structured answers, went and explored the code myself, used the hints they'd given me to validate everything, and wrote up a comprehensive document explaining the lot.

## Naive me thought job done

Obviously I was not done. You'd think by now I'd know better.

A week later the contracting team came back with "cool, we have a plan." They'd taken everything I'd given them, created architectural diagrams, Confluence documents, and actual thinking. They wanted me to review whether their approach would work.

So I did the same thing again. Took their documents, the context I'd already built, and pointed all three AI harnesses at the relevant repositories, not just mine but across four different teams' repos, backend services and frontend services and everything in between. I had each one validate whether what the contractors were proposing would actually work. Then I took the outputs from all three, wrote them to file, and had a fourth agent (OpenCode running Opus 4.6) synthesise a combined result. I used that synthesis to structure my response back to the team.

I've now done this process three times. Here's how it works:

> **The Council Process**
>
> 1. Gather context and documentation
> 2. Structure a comprehensive prompt
> 3. Run the same prompt through multiple AI agents and let each investigate the repositories independently
> 4. Save their structured outputs
> 5. Run a synthesis agent across all results
> 6. Validate manually: use the AI outputs as a map for where to look, read the code yourself, and run quick targeted questions past other engineers

## Where the real value lives

The synthesis step is where the magic happens. It's not just about getting three answers. It's about what happens when you put them next to each other.

The synthesising agent highlighted where all three harnesses were in agreement, which gave me confidence. But more importantly, it highlighted where they'd noticed different pieces of the problem. Even though they were looking at the same repositories and most likely using the same underlying tools, they ended up pulling out different things. Codex might flag an endpoint I hadn't considered. Claude Code might trace a data flow the others glossed over. The breadth of coverage from running three agents was meaningfully wider than any single one.

This also feeds into something that should be obvious but bears repeating: AI hallucinates. You cannot 100% commit to trusting just one version. When you need accurate architectural understanding, having multiple agents give you a synthesis that you then validate yourself is genuinely useful. It's not a replacement for reading the code. It's a way to read the code faster and know where to look.

## The tools have personalities

Here's something I find fascinating, and I'm not the only one. Another principal engineer I know has noticed the same thing.

Codex is the grumpy pragmatist. It goes away, gets some stuff done, comes back, and tells you the bare minimum you need to know. Not a single detail more. Bullet points, to the letter, done. That's fine. That's exactly what you'd expect from a tool optimised for task completion.

Claude, given the exact same prompt via the web with Opus, comes back reading like a chatty engineer. A bit scattered, a bit flowery, but thorough. You'll get everything you need, it'll just need a bit of back-and-forth to extract it cleanly.

But here's the interesting bit: OpenCode, regardless of which model it's running underneath, whether that's Opus or GPT-5.4, tends to give better structured results than either of the first-party platforms running the same models. The investigations are better organised. The outputs are clearer. The intent comes through more directly. I'm finding this is true when comparing Claude Code to OpenCode running Opus, and it's also true when comparing Codex to OpenCode running GPT-5.4.

## The harness matters more than the model

The scaffolding around the model, how it structures tool calls, how it formats its output, how it organises an investigation, is doing more heavy lifting than people assume. That's a genuinely counterintuitive finding. The same model, in a different harness, produces meaningfully different quality of output. If you're only evaluating models, you're missing half the picture.

## AI expands capacity, not energy

I'll be honest. By the end of every week right now, I am flattened. Exhausted. Mentally, emotionally, everything. Gone.

These tools have enabled me to explore and understand systems at a superficial level far faster than I ever could otherwise. To get the depth I needed for these handover documents would have taken weeks of investigation. I did it in hours. That's real. That's meaningful. That capacity expansion let me keep working on high-priority deep-dive bugs while simultaneously supporting an external team and ensuring they had enough context to be unblocked and start working independently.

But working with AI at full tilt is cognitively expensive in ways that people underestimate. You're doing more, faster, and that uses more of your mental energy than you think. AI gave me the capacity to do work that would've been impossible to fit in otherwise. It did not give me more energy to do it with.

## Still experimenting

I've run this playbook three times now without changing it. Same process each time. I haven't tried to refine it or automate it or build a harness around it yet, though it's in the back of my mind. I actually started building a mobile app a while back to formalise the council concept for personal use, but got distracted because, well, reasons.

So what's the lesson? Don't trust one AI. Use a council. Get them to validate each other. Get them to look for reasons they're wrong. Use the synthesis of multiple perspectives to build confidence in your understanding, then go validate it yourself.

I'm still not entirely convinced this is the best strategy. But it is letting me do things I could not have done otherwise, and right now that's enough. The future of AI-assisted engineering might not be a better model. It might be a better council.