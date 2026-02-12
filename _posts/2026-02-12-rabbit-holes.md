---
layout: post
title: "14 PRs, 6 Repos, 1 Button: A Tale of Tumbling Down the Rabbit Hole"
date: 2026-02-12 08:00:00 +0000
categories: vibecoding claudecode specdrivendevelopment codex
---

_True stories from the front lines of the internet..._

---

![Alice falling down the rabbit hole](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Down_the_Rabbit_Hole_%28311526846%29.jpg/960px-Down_the_Rabbit_Hole_%28311526846%29.jpg)
*Alice in Wonderland by [Valerie Hinojosa](https://commons.wikimedia.org/wiki/File:Down_the_Rabbit_Hole_(311526846).jpg) / [Creative Commons Attribution-Share Alike 2.0
](https://creativecommons.org/licenses/by-sa/2.0/)*


Now this is a story all about how one button link got my codebase flipped turned upside down. And I'd like to take a minute, just sit right there, and I'll tell you how I shipped 14 PRs without pulling out my hair.

It started with a Monday morning meeting. I'd been off for three weeks. The meeting was dense with context about decisions made months ago, documented across scattered specs and design docs. Systems I don't own. Plans originally speced out almost a year prior. SEO requirements. Legacy middleware behaviour. And somewhere in all of this, a single task: change where a subscribe button points.

The old flow routed users through a legacy auth endpoint which was a piece of middleware handling user state and return-to-site functionality. The new flow should skip that layer and go direct. Simple, right?

Three repos. 3 small PRs. That was the original scope.

It became six repos and one or two more PRs...

## The Context Problem

Here's what made this tricky: I didn't have the context. Not the institutional knowledge of why things were built this way. Not the codebase familiarity to know where all the tendrils reached. Not the cross-system visibility to see how changes would ripple.

Normally, this is where you'd involve other teams. Schedule alignment meetings. Negotiate architecture choices. Coordinate timed releases. The org chart becomes the constraint.

Instead, I threw five AI tools at the problem.

I used internal knowledge search to surface half a dozen docs from a year ago about what a potential migration might look like. Copilot and Codex scanned repos I'd never opened, outputting high-level analysis of what would need to change. NotebookLM synthesised a dozen-plus sources into actionable Jira tickets with acceptance criteria and testing plans. And Claude handled the actual implementation across all six repositories.

Each tool for what it does best. None of them sufficient alone.

## The Shape of the Change

What was supposed to be three repos became six because the AI tooling kept finding rabbit holes worth going down.

The approach was backwards compatibility first. I updated the auth service to forward requests to the new endpoint, so existing systems would keep working. Only after that was stable did I remove the old code paths and switch the calls to point directly to the new flow.

Along the way, I hit a referrer bug that only revealed itself mid-implementation. One of the components lived in a shared library, not a full application, which meant handling referral data differently than expected. This meant that I had to change how it was reading from window referrer data rather than relying on direct redirect URLs.

And then there was a shared header component in another team's repo. Hardcoded to the old endpoint. In code I couldn't easily modify. The rabbit holes kept cropping up every time I thought I dived down them all. 

Fourteen PRs. Six repositories. Backwards compatible throughout. Zero downtime.

The old flow had an extra hop through legacy middleware that handled state management. The new flow removes that layer entirely. Which makes for a faster time to checkout, same user experience, one less thing to maintain.

## The Point

This would have been a multi-team effort. Alignment meetings across three teams, at minimum. Negotiated timelines. Architectural discussions. Coordinated releases.

Instead, it was one developer holding context that used to require an org chart.

I'm not saying AI tooling makes you a better engineer. I'm saying it lets you hold more context. And sometimes that's the difference between "we'll need to schedule a meeting with the other teams" and "I'll have a PR up by Thursday."

The context ceiling just got a lot higher.