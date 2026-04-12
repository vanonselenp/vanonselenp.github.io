---
layout: post
title: "The Canary in the Harness"
date: 2026-04-12 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_On discovering that your favourite tool got measurably worse, that you'd been blaming yourself for it, and that the only reason you noticed at all was because another harness was sitting right next to it behaving normally._

---

![The Canary in the Harness](/assets/canary-hero.png)

## A tale of two Ralph loops

A couple of weeks ago I was playing with Newshound, a personal project of mine that pulls together a digest of interesting things from a list of about thirty sources on the internet. I wanted to add a feature that was a little more involved than the usual yak shave. Spec conversation. PRD skill. JSON. Ralph loop. The full ceremony.

I ran the loop in Claude Code. It went for two hours. A good chunk of that two hours was Claude Code recursively chewing on the same problem, half-finishing things in slightly different ways each time around. Eventually it limped over the finish line. At which point my Pro subscription tapped out.

I went off and set up the wrapper script from [the last post](https://www.petervanonselen.com/2026/04/11/the-grand-plugin-trap/) to allow me to run a Ralph loop on OpenCode. I then ran the *exact same prompt* through OpenCode with GPT-5.4. Same Ralph loop. Same PRD. Same instantiation of the problem.

Fifteen minutes.

I noticed this. Of course I noticed this. And the conclusion I reached, the one anyone would reach, was: huh, GPT-5.4 must just be better at this particular kind of task. I filed it under "interesting data point about model personalities" and moved on. I'd written about how each harness has its own character in [the council post](https://www.petervanonselen.com/2026/04/03/the-council-will-see-you-now/), and this felt like more of the same. Different tool, different shape, sometimes one fits the keyhole better than the other. Cool.

That was the wrong conclusion. I just didn't know it yet.

## What Newshound put on my desk

Two days ago Newshound surfaced [a GitHub issue](https://github.com/anthropics/claude-code/issues/42796) on the Claude Code repo. There is a particular pleasure in your own tool catching the thing that's about to reframe how you think about your other tools, and I want to note it before I move on, because the whole point of personal projects is moments like this.

The issue was filed by Stella Laurenzo, an engineer working deep in the AMD GPU compiler stack on IREE. Not a casual user. Not someone shouting into the void about vibes. Someone whose day job is to run dozens of concurrent Claude Code agents against a non-trivial systems codebase, who logs everything, and who knows how to do statistics to data.

The headline finding is brutal. From late January through early March, she analysed 17,871 thinking blocks and 234,760 tool calls across 6,852 Claude Code session files. What she found is that somewhere between mid-February and early March, Claude Code's behaviour changed in measurable, reproducible, machine-readable ways.

The number that broke me is the Read:Edit ratio. In the good period, Claude Code was reading 6.6 files for every file it edited. By mid-March, that ratio had collapsed to 2.0. The model stopped reading code before changing it. One in three edits in the degraded period was made to a file the model hadn't read in its recent tool history.

There's more. A "stop hook" she built to programmatically catch Claude trying to dodge work, ask unnecessary permission, or declare premature completion fired 173 times in seventeen days. It had fired zero times before March 8th. Zero. Every phrase in that hook was added in response to a specific incident where Claude tried to stop working and had to be forced to continue. The word "simplest" in Claude's outputs went up by 642 percent. The word "please" in *her* prompts dropped 49 percent. The word "thanks" dropped 55 percent. She stopped being polite to it because there was nothing left to be polite about.

The methodology is more rigorous than anything I would ever bother to do, the dataset is enormous, and the appendix where Claude Opus analyses its own session logs and writes "I cannot tell from the inside whether I am thinking deeply or not" is one of the more haunting things I've read in a technical bug report.

Go and read it. I'm not going to recap the whole thing. The point that matters for this post is much smaller and much more personal.

## The thing I'd been blaming on myself

I have been using Claude Code since June last year. In that time it has been, without much competition, the most enjoyable engineering tool I've ever used. The blog you're reading exists in part because of how much I have wanted to write about working with it.

But over the last few weeks something had been off. Sessions felt slower. The chatter I was used to, the running commentary where Claude Code would talk through its plan as it worked, had gone quieter. The two-hour Ralph loop on Newshound was the loudest version of it but it wasn't the only one. I'd had a couple of sessions where it felt like Claude was rushing to a conclusion, where the reflection phase produced shallower answers than I was used to, where I was correcting more and praising less.

I had put all of this down to me. I'd been burnt out and needing a holiday. I was probably tired. I was probably prompting badly. The problem was probably harder than I'd estimated. The Ralph loop was probably a poor fit for the task. GPT-5.4 was probably just better at this particular slice of work.

None of those things are unreasonable explanations. They're the kinds of explanations a senior engineer reaches for first, because the alternative, "the tool I rely on every day got measurably worse without telling me," feels paranoid and slightly embarrassing. So you eat it. You assume the variable that changed is you.

And then someone with 6,852 session logs and a Pearson correlation coefficient publishes the receipts, and you sit there reading them on a Sunday afternoon thinking: oh. Oh, that's what that was.

## The argument the council post wasn't making yet

When I wrote about [convening multiple AI harnesses as an architectural review council](https://www.petervanonselen.com/2026/04/03/the-council-will-see-you-now/), the pitch was about getting better answers. Different harnesses have different personalities, the harness matters more than the model, three opinions plus a synthesis beats one opinion. All of that I still believe. But there was a second argument hiding in there that I didn't see at the time, and Stella's report is what dragged it into the light.

Multi-harness working is regression detection.

It is, for most of us, the *only* regression detection we are ever going to have. I am not going to instrument my Claude Code sessions, capture 234,760 tool calls, and run a signature-length correlation against thinking depth. I have a day job and a stealth tactics game to build. Stella did that work and the rest of us are in her debt for it, but it is not a repeatable practice for anyone whose job title isn't "compiler engineer with infinite patience and a logging fetish."

What *is* repeatable is keeping three harnesses in active rotation and noticing when one of them starts feeling off relative to the other. The fifteen-minutes-versus-two-hours moment with Newshound was a regression signal. I just didn't read it as one because I had no framework for the idea that the harness itself might be the variable. I assumed harnesses were stable. They are not stable. They are moving targets, reconfigured continuously by people who do not write to you about what they changed, and the only way you find out is by holding two of them up to the same problem and watching one of them flinch.

This is what the plugin trap was protecting against without me fully understanding why. [Yesterday's post](https://www.petervanonselen.com/2026/04/11/the-grand-plugin-trap/) was about keeping the exits visible so you don't get locked into a single ecosystem. The thing I didn't say, because I didn't know it yet, is that the room you're standing in is being remodelled while you sleep. Exits aren't just for when you want to leave. Exits are how you find out the room has changed shape.

If your entire workflow lives inside one harness, harness drift is invisible to you. It just feels like you're having a bad week. You blame yourself. You prompt harder. You write longer CLAUDE.md files. You assume the problem is on your side of the screen, because from inside one harness there is no other side of the screen to compare against.

## Naming names, because this is supposed to be honest

I am going to name Claude Code directly here, because this blog only works if I'm being truthful about what I'm actually using.

The tool that got measurably worse over the last month is Claude Code. The tool I have loved more than any other engineering tool in the last decade is Claude Code. Those two sentences belong in the same paragraph. I am writing this *because* of how much I like the thing, not in spite of it.

If you have been feeling like Claude Code is harder to work with than it was in February, you are probably not imagining it, and you are probably not getting worse at your job. There is data. The data is good. Go and read it.

## What I'm taking away

Three things, and then a rabbit hole.

First, I want crude metrics on my own harness usage. Not 234,760-tool-call-Pearson-correlation crude. Just crude. How many tool calls per session. How many file reads versus file edits. How many times I had to interrupt and correct. Even a daily tally of "did Claude Code feel like it was trying today" would be more signal than I currently collect, which is zero. If the regression signal is detectable in aggregate, I want to be looking at the aggregate.

Second, I want a smoke-test prompt suite. A handful of canonical prompts that exercise the kinds of work I actually do, that I can run across harnesses on a rough cadence and use as a tripwire for drift. Nothing fancy. A small fixed battery, run weekly, results scribbled in a notebook. The point is not the rigour, the point is the comparison over time. I have been operating without a baseline and it has cost me.

Third, the portability argument from the plugin trap post upgrades from "useful insurance against rate limits and lock-in" to "the only way you will ever notice that your tools have silently changed underneath you." Multi-harness working is the canary. If your canary is the same species as the thing you're trying to detect, you don't have a canary. You have another bird in the same mine.

And then the rabbit hole.

## The next room over

There is a project called [pi](https://pi.dev) by a developer named Mario Zechner. The tagline on the front page is "There are many coding agents, but this one is mine," which is doing a lot of work in eight words. Pi is a minimal, aggressively extensible terminal coding harness. The pitch is that you adapt pi to your workflow rather than the other way around. No sub-agents, no plan mode, no built-in todos, no MCP, no permission popups, no background bash. All of those things are extensions you add, or build, or install from someone else's package. The core stays small and the shape comes from you.

There is [a YouTube video](https://www.youtube.com/watch?v=Dli5slNaJu0) by Mario walking through how he came to build it that I have not yet found the time to fully watch, and this post is partly me giving myself permission to find that time.

The reason pi feels like the natural next thing is that it is the logical endpoint of an argument I've been making in pieces across the last few posts. The plugin trap post said your workflow shouldn't live inside one harness. The council post said different harnesses give you different answers. This post is saying different harnesses give you the only honest baseline you have for spotting drift in any one of them. The next move, the move I cannot stop thinking about, is: what if the harness itself is something you own? What if instead of being a tenant in three different rooms, all of them being remodelled by other people on different schedules, you build a small room of your own, with the doors where you want them, and treat the rented rooms as the comparison set?

I do not know yet whether pi is the right answer to that question. I have not run it. I have not watched the video. I have a game and a new digest agent I am supposed to be working on, and the smell of yak around me is already pretty thick.

But I can feel the next dive coming. And after the week I've just had, I am done pretending that holding still inside a single harness is the safe choice. The safe choice is having somewhere else to look from.

Off I go.