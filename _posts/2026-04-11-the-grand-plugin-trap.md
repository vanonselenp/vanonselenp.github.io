---
layout: post
title: "The Grand Plugin Trap"
date: 2026-04-03 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_In which our narrator, locked out of his usage limits on holiday, learns that every grand hotel has only one front door._

---

It's day two of my holiday and I'm staring at a Claude Code session that won't do anything. Pro limit hit. Three days until it resets. There's a personal project sitting open in another window that I'd been quite enjoying poking at, and now I can't poke at it, and the bit of my brain that had been having a perfectly nice time is suddenly very loud about the £20 of extra credit I'd burned through in a single afternoon earlier in the week.

This is the story of how that lockout forced me to do a small piece of unglamorous setup work I'd been avoiding for months, and what I found on the other side of it.

## The workflow

Quick context. Over the last nine or ten months I've fallen into a working rhythm with my personal projects that goes something like this. I open an AI chat, and I have a long conversation with it. Not a "write me some code" conversation. A "let's interview each other about what I'm actually trying to build and why" conversation. These run for three or four hours sometimes. Lots of back and forth, lots of poking at scope, lots of trying to find the smallest version of the thing that would actually tell me whether the idea is any good. At the end of all that I have what I've been calling a spec: a high-level document about what we're doing and why.

Then I take the spec and run it through a PRD skill I shamelessly stole from the Ralph loop. Quick aside: PRD is a term I had genuinely never encountered in fifteen years of working in agile teams. I first heard it watching YouTube videos about people working with AI, sometime in the last year, and I had to go and look up what the bloody hell it stood for. As best I can tell, a PRD is an epic with a collection of user stories, some acceptance criteria, some functional and non-functional requirements, and a bit of product context bolted on top. Cool. I can work with that. The reason I like this particular PRD skill is that after I've already spent four hours on the spec conversation, it asks me five more questions to validate what I'm building. Which is exactly the kind of thing you want at that stage!

PRD becomes JSON. JSON gets fed to a Ralph loop. Off we go.

## The bit where I was cheating

Here's the dirty secret. I'd never actually set up the Ralph loop the way you're supposed to set it up. I'd been running it via a plugin inside Claude Code. Plugins are wonderful. You install them, they work, you're productive in ninety seconds. Why would you write a bash script when you can install a plugin?

The honest answer is: you wouldn't. And that's the trap. The problem isn't plugins. The problem is when your workflow only exists inside one of them.

Plugins feel like the harness rewarding you for committing to it. Every plugin install is a small vote for staying inside that one ecosystem, and those votes compound quietly until one day you look up and notice you've stopped being portable. You're not running a workflow anymore. You're running a workflow *that only exists inside Claude Code*. Which is fine, until it isn't.

## How I burned through the credits in the first place

I should be clear about something. I hadn't hit the Pro limit doing serious work on my personal project. I'd hit it because it was my holiday, and I'd spent the previous week happily down an oh-my-codex rabbit hole for no reason other than that it was interesting.

Oh-my-codex is a sprawling wrapper that someone has built around Codex to give it brainstorming flows and Ralph loops and a pile of other usability niceties. I'd become curious about it for a very specific reason: when the Claude Code source leaked, a developer in South Korea used Codex with oh-my-codex to reimplement the entirety of Claude Code in Python. In six hours. *Six hours*, for a non-trivial codebase. I wanted to understand how that was even possible, which meant I wanted to make oh-my-codex work with OpenCode and Claude Code rather than just Codex, because of course I did. More harnesses. Always more harnesses.

![the way](/assets/grand-plugin-trap/the-way.png)

So that's what the credits went on. A week of trying to bend an already-baroque wrapper around two more harnesses it wasn't designed for, purely because I wanted to know how the thing worked. No deliverable. No project at the end of it. Just the kind of dive-in-and-poke-at-it exploration that holidays are for. I was having a great time, the plugin inside Claude Code was still humming along for the actual personal project I dipped into between rabbit hole sessions, and the cost of any of this hadn't shown up yet.

Then it showed up.

## The thing I'd been ignoring at work

I should have seen this coming, because at The Economist I have access to three different coding agents with three different usage pools, each gated on different constraints. In practice that means I bounce between them all day. Hit a five-hour window in one, switch to another, work until that one taps out, switch to the third. It's a genuinely lovely setup if you're the kind of person who likes being spoiled for choice on tokens.

But it also means I've been quietly reinstalling the same plugins and the same markdown scripts in three different places, every time something changes. And whenever one of those environments goes down or gets reconfigured, I lose half a morning rebuilding the workflow in another one. I'd been feeling that friction for ages without ever quite naming it. It was just background noise. The cost of doing business.

Then the personal Pro lockout happened, and suddenly the background noise was the only thing in the room.

## Doing the unglamorous thing

So I went and found [open-ralph-wiggum](https://github.com/Th0rgal/open-ralph-wiggum), worked out how to wire it up properly, and wrote [a small zsh function](https://github.com/vanonselenp/zsh-functions/blob/main/functions/ralph-loop.zsh) that wraps it so I can just type `ralph-loop` from any project directory and have the thing kick off without me having to remember any flags. None of this was hard. None of this was interesting. It was the kind of work I had been actively avoiding because I'd already spent a week earlier that month fiddling around with Codex and OpenCode and trying to make various things play nicely together, and the last thing I wanted was *more* yak shaving.

But here's the thing about doing it during a forced lockout, with nothing else to distract me. There was nothing else to do. So I sat with it. And once it was done, I had a Ralph loop that ran on top of OpenCode, with GPT-5.4, completely independent of whether Claude Code was up, down, or rate-limited into oblivion. The wrapper meant I could move between harnesses without rebuilding anything. The script lived in my dotfiles. It was just *there*.

## The real prize

I've [written before](https://www.petervanonselen.com/2026/04/03/the-council-will-see-you-now/) about how each AI harness has its own personality. Claude Code thinks differently from Codex thinks differently from OpenCode, and a lot of that personality lives in the harness rather than the model. I still believe that. But what I hadn't fully clocked, until this week, is that everything I'd written about harness personalities was manual copy paste painful exercises, because the plugin had me boxed into one of them.

Knowing the council exists is one thing. Being able to actually convene it on a Tuesday afternoon while you're trying to ship something is another. The wrapper script is the thing that closes that gap. It allows for more meaningful agentic workflows in any harness easily.

That's the prize. Not the lockout workaround. Not the bash script. The portability that lets the multi-harness thing actually be a way of working rather than an essay.

## What I'm sitting with

I'm going to keep using plugins. They're genuinely useful and I'm not about to LARP as someone too principled to install convenient things. But I'm going to be more suspicious of how easy they make the first ninety seconds feel, because I now have a much clearer sense of what they cost on the back end. Every plugin ecosystem is a small gravity well. The more you commit, the harder it is to leave, and — this is the part that bothers me most — the less you can even see what you're missing on the outside.

The unglamorous wrapper script turns out to be a small act of resistance against that. Not a heroic one. Just a vote for keeping the exits visible.

I'd rather have the exits visible.