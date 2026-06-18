---
layout: post
title: "The Machine Had Been Keeping a Diary"
date: 2026-06-12 06:00:00 +0000
categories: claudecode opencode softwarecraftsmanship
image: /assets/machine-diary-hero.png
thread: craft
tags: [ai-assisted-engineering]
---

*Burn the land and boil the sea; the skills, I hope, come with me.*

---

![The Machine Had Been Keeping a Diary](/assets/machine-diary-hero.png)

I wrote a while back that [skills are compressions of workflow](https://www.petervanonselen.com/2026/05/23/i-didnt-grok-superpowers/), and that importing someone else's rarely works because you never earned the patterns underneath. It took me until this month to notice it has a blindingly obvious second edge. If you asked me to describe my own workflows, the ones I would presumably be compressing, I could not have done it.

In my defence, the conditions for noticing have not been great. Since early spring I have been running at an intensity that leaves no room for the kind of reflection that wants a quiet afternoon and a notebook. Meta-thinking about process is the first thing that dies when every day contains three urgent things and no lunch. I knew, in the abstract, that months of daily work with Claude Code and OpenCode must have worn grooves into how I operate. I had no idea what the grooves looked like.

So I did the obvious lazy thing. I asked the AI to tell me.

> I want to do a high level broad based analysis of usage patterns of OpenCode and Claude Code on this computer. Things I want to know: skills and agents that should have been written to simplify processes that were missing, how could I have done better, what did go well. Ask me questions.

A few iterations later I had a proper report. The raw material was all just sitting there: sixteen weeks of history, 643 sessions in one harness and 87 in the other, nearly 25,000 tool calls, 1,787 distinct prompts. The machine had been keeping a diary on me the entire time. I had simply never read it.

Two findings stood out, and both were things I had done without noticing.

## The agents file I forgot I wrote

Some context. I have a workspace containing the repositories I have had to touch as a staff engineer over the last nine months: more than thirty of them, many owned by other teams. The work spans TypeScript, Go, Salesforce, frontend apps, backend lambdas, container deployments, shared component libraries. It is too much context to hold in my head, and I would expect an AI harness to fall over trying to hold it in its context window too.

One Friday afternoon, while poking at pi.dev to see what it could do, I had it write an AGENTS.md for the workspace folder. Not for a repo. For the folder of repos. A digest of what each one is, what it talks to, and how to interact with it. Just enough for an agent to navigate across domains, not so much that it drowns. Then the weekend happened, and by Monday I had completely forgotten I had done it.

The analysis singled that file out as one of the most effective things in my entire setup. Cross-repo investigations started from a real baseline instead of a cold one. Fan-out exploration got cheaper and sharper. The cheatsheet section mapping which kinds of change ripple into which repos had visibly prevented mistakes. The report called the file genuinely good, which from a machine grading my homework felt weirdly like getting a gold star.

The accident is now deliberate, at least mostly. The agents file has [a skill of its own](https://github.com/vanonselenp/skills/blob/main/skill/maintain-workspace-agents-md/SKILL.md) now, one that audits the digest for drift against what is actually on disk, proposes a diff, and waits for me to accept it. The weekly cron job that would make the refresh automatic is still on the to-do list. The thing I did by fluke on a Friday afternoon is now something that happens on purpose. Nearly.

## The ritual I did not know I had

I already had a pr-review skill. I wrote it months ago. It analyses a changeset and flags red flags, blockers and should-fix issues, and I was reasonably proud of it.

What I had not noticed is that the skill was one step in a five-step ritual I performed every single time. Pull the branch into a fresh worktree. Run the review pass. Read the ticket to understand what the change is actually supposed to do, because a diff that is internally consistent can still be solving the wrong problem. Have the AI compress everything it found into a handoff document. Then take that document into a clean context and revalidate it, tracing the code paths through every layer and checking the change against the patterns that already exist in the codebase.

The report put a number on it. The pr-review skill had been loaded 92 times. The next most used skill in my entire setup had been loaded ten. Ninety-two repetitions of a ritual I would have told you, honestly, that I did not have. The skill I was proud of covered one step out of five, and the other four lived nowhere except my fingers.

So I wrapped the whole ritual in [a skill](https://github.com/vanonselenp/skills/blob/main/skill/pr-review/SKILL.md), and the timing was almost cruel. My final weeks at The Economist, and final is still a strange word to type, were almost nothing but review. Large AI-assisted pull requests, arriving faster than any one person was ever meant to read them. All day: read code, leave comments, read more code. The wrapped skill is the only reason my feedback stayed consistent at a volume where consistency is normally the first casualty.

## The diary does not flatter

The report had less comfortable things to say too. I had been writing every review document to a macOS temp directory that evaporates on its own schedule, then paying to re-derive the contents in the next session. One afternoon I launched fourteen review subagents in a three-hour window and each one independently re-fetched the same diff, which is how you burn fifteen dollars re-reading yourself. And the agent's clarifying questions got dismissed by me nearly a fifth of the time, which on inspection was not the agent being stupid but me never telling it that when a sensible default exists, it should pick one and say so rather than asking. It turns out a decent share of my complaints about the tool were really complaints about instructions I had never written.

None of this was visible from inside the work. Which is, I think, the actual point. The data was sitting in a SQLite database and a folder of JSONL files the whole time, a complete record of sixteen weeks. What was missing was the step back, and the step back is exactly what a certain kind of busy makes impossible. An afternoon of having an AI interrogate my own usage bought me the sort of retrospective I would otherwise need a sabbatical and considerably better discipline to attempt. It found things that no amount of in-the-moment attention was ever going to surface, because habits are precisely the things you stop seeing.

## The diary stays behind

There is a less comfortable thought underneath that one, though. Everything the analysis surfaced is a compression of this job. The agents file describes a workspace I no longer have. The review ritual is fitted to one codebase ecosystem, one ticketing convention, one team's way of working. I have spent months arguing that you cannot adopt someone else's skills because you did not earn the patterns underneath them. Soon I start somewhere new, and I get to find out which side of my own argument I am standing on. Maybe the patterns are mine and they travel. Maybe they belonged to the job, and next-job me is the someone else, arriving with a folder of skills he did not exactly earn. I am apprehensive about that. I am also, genuinely, looking forward to finding out.