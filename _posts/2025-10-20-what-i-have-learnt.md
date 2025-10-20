---
layout: post
title: "From AI Skeptic to Constant Collaborator: What I Learned Vibe Coding"
date: 2025-10-20 08:00:00 +0000
categories: personal board-game godot video-game claudecode codex vibecoding
---

_The Question That Started Everything... am I going to lose my job?_

---

## The Question That Started Everything

How does one actually vibe code? And the follow-on questions that kept me up at night: Is it any good? Can I actually generate real code with this? Is this going to take my job? Am I running out of career runway?

Around the start of June this year, I was an AI optimist while not really engaging with it. I used ChatGPT, DeepSeek, and Anthropic's Claude, ran some thinking through them, maybe did basic searches. Honestly, I wasn't using it in any meaningful way. Functionally, I was just playing with it. Nothing more.

Then I got stuck on a problem. By simply following my curiosity, I went from not having a clear idea of what I wanted to accomplish with AI to actively using it as a constant collaborator across multiple domains of my life. My approach to AI has fundamentally changed over the past four months, and it continues to evolve.

## The Catalyst: Magic the Gathering (Naturally)

**TLDR**: I tried to make a [Jumpstart cube](https://vanonselenp.github.io/2025/08/04/jumpstart-cube-catastrophication/). ChatGPT couldn't solve it. Co-pilot couldn't solve it. Co-pilot vibe coded a solution that kinda worked. I vibe coded a new solution that actually worked.

I couldn't get the damn thing out of my mind, so I vibe coded this [portfolio site](https://github.com/vanonselenp/vanonselenp.github.io) to document what happened. Then, while working on the cube, a [board game idea struck](https://vanonselenp.github.io/2025/08/21/sky-islands/), and I couldn't get it out any other way except by building it with AI. That board game has somehow [morphed into a video game](https://vanonselenp.github.io/2025/09/07/boardgame-to-digital/) that's far too complicated for the "get an MVP into prod fast" approach I keep trying to follow.

**The time investment**: 1-2 hours a day, either in the morning before work or while watching TV with my wife in the evening. This became an all-consuming obsession for four months. I sacrificed learning urban sketching, which I'd spent the first half of the year actively pursuing.

**The cost**: I'm paying £16/month for Claude Pro and £20/month for ChatGPT Pro. I use Claude as my primary coding assistant and switch between ChatGPT and Claude for thinking through problems. It's worth it, without AI, none of these projects would exist.

Pre-AI, my side projects were timeboxed to a couple of days and small, achievable problems. Anything more would rapidly collapse under its own weight, too much code, too little time. Basically I didn't do tech side projects. AI changed that equation entirely.

![pre ai assisted tooling](/assets/github.png)

## What I've Learned: The Core Insights

### AI is a Tool and a Multiplier

You have to treat AI not as a magic box that will automatically solve whatever you hope it does, but rather as another person you're working with over Slack. If you tell a coworker "make me a feature!" you can't be upset when they return junk.

The best way to use this tool is to assume it doesn't actually know what you want. I've found the most effective approach is to start conversations with lots of negative validation questions: What am I missing? What could be improved? Be critical. Be objective. Get the AI to shoot holes through your ideas.

Once you've had this conversation, write that plan to file. Congrats, you now have a high-level plan. This becomes useful context for future chats. However, this alone won't give you consistent, reasonable, progressive progress. Because basically, AIs like to write code, and they write an awful lot of it.

So get it to make a todo list with a painful amount of tick boxes.

![checklists!](/assets/checklist.png)

When building, use that todo document to hold the AI accountable. It makes testing and building more predictable and manageable.

### The "Junior Engineer" Mental Model Goes Deeper Than You Think

Treating AI like a junior engineer isn't just about tone, it's about workflow. Through my projects, I discovered I needed to:

- **Use different AIs for different roles**: ChatGPT for exploration and brainstorming, Claude for implementation and code review
- **Create specs as "shared memory"**: Documentation that gets committed to the repo so the AI can reference it across sessions
- **Break work into granular todos**: Not just for you, for holding the AI accountable to what actually matters
- **Pair with it through code review**: Not just generation

This evolved from my Magic cube project where I had specs numbered 1 through 15, each documenting a feature discussion. These weren't outputs, they were context that survived beyond individual chat sessions.

## The Dangerous Patterns: What They Don't Tell You

### The Refactor Paradox

Here's something crucial I learned the hard way: **AI accelerates the "green" phase so much that you skip "refactor," leading to massive technical debt.**

During my Magic cube project, I went from manually patching decks to having a 10,000-line IPython notebook that was completely impossible to understand. I had hit cognitive overload.

As an ardent TDD advocate in my day job, I realized I was missing two critical pieces of the red-green-refactor cycle: I was just writing code. No tests. No cleanups. Rookie mistake.

I had to start from scratch, consciously embracing a build-and-refactor loop, following the code smell patterns that years of clean code practices had drilled into me. AI doesn't just multiply your output, **it multiplies your technical debt if you're not careful.**

The game dev project repeated this pattern. I'd run `git ls-files | grep '\.gd$' | xargs wc -l` and see files well over 2k lines. I'd missed refactor cycles again.

### The Tangent Amplification Problem

AI doesn't just enable scope creep, **it actively encourages it by making every side quest feel achievable.**

My board game project is the perfect example. I set out one week to work on creature combat. By the end of the week, I had:
- Created test creatures
- Built movement and attack systems
- Added height-based defense
- Implemented dice roll combat
- Created a radial menu for unit actions
- Downloaded 3D models from Kenney.nl
- Rebuilt roads with proper models and rotations
- Added a blink ability

One feature became an ecosystem. And here's the thing: **it is beyond exceedingly simple to wander off on completely unrelated tangents** when the AI makes everything feel possible.

I kept telling myself "get an MVP to prod fast" while simultaneously building procedural island generation with Wave Function Collapse algorithms. 

But here's why I didn't stop: **AI provides so much momentum that even when it's frustrating, you can think about the problem slightly differently and feel like you're making progress.** When direct AI generation hits a wall, I switch to having it build the broad structure while I manually tweak settings. This makes working on side projects genuinely fun in a way they haven't been before.

The momentum AI provides is a double-edged sword. It keeps you engaged through the frustration, but it also keeps you building when you should be stepping back and asking "is this the right thing?"

### The Direction Problem: AI's Spatial Blindness

Some tasks reveal AI's sharp limitations. During my road system implementation, I discovered that **AI spatial reasoning is terrible.**

When work involves orientation, rotation, or physical space, the AI's sense of direction doesn't match how the world is rendered. Trying to explain rotations in a way that makes sense to both of us is like teaching a goldfish to drive.

And if the AI ever accidentally gets something right, it will immediately overwrite it in the next change.

My eventual workflow:
1. Get the AI to build the big stuff, toggles, switches, base structure
2. Manually go through and tweak everything myself

This led me to develop what I call "Git [save-scumming](https://tvtropes.org/pmwiki/pmwiki.php/Main/SaveScumming)", treating Git like a video game save system because AI will thoughtlessly overwrite correct solutions without remembering what worked.

## The Momentum Trap

AI gives me the same benefit I get from using Audible for reading books: **momentum**. It's a lot easier to keep working on a side project with AI than without, especially when you have no time at all to do the work.

But here's the tension my blog posts reveal: momentum without direction leads nowhere useful.

I built 24,000 lines of Python code for a board game that probably should have been paper prototyped first. I kept reminding myself to "get an MVP to prod fast and learn lessons," but the AI made it so easy to keep building that I kept following the fun instead of following the plan.

The momentum is addictive even when it's pulling you away from your goal. You have to be disciplined about direction, or you'll end up with beautiful code for the wrong thing.

## The Transformation: Four Months, Everything Changed

The most remarkable thing about this journey isn't what I built, it's the speed of transformation.

**June 2025**: AI optimist, barely engaging
**October 2025**: 24k lines of game code, active collaborator across multiple projects, writing blog posts documenting the journey in real-time

Getting to the "treat AI like a junior engineer" mindset took about 2-3 weeks. I had to unlearn the "AI is magic" assumption and figure out how to actually use it.

This wasn't gradual learning, it was catalytic. Each success made the next leap feel possible:
- Magic cube problem → vibe coding solution
- Couldn't stop thinking about it → portfolio site
- One blog post → entire blog series
- Board game idea → 24k lines of video game code
- Video game reimplementation → another 24k lines of video game code

The cascading confidence is real. Once you see AI help you solve one "impossible" problem, you start seeing possibilities everywhere.

## Bringing It Back to the Day Job

The spec-driven workflow I developed through these side projects has now become how I work professionally. I take tickets and reframe them into specs with task breakdowns. I use AI to analyze complex codebases I'm barely familiar with.

Right now I'm refactoring a monolith written in Go into a commons library with five microservices, using the AI spec-driven workflow with AI-assisted code development, working in small increments. Everything I'm doing, I learned from these side projects.

The irony: The Economist (where I work) has embraced AI tooling internally, while engineers in general remain reticent. I get it, I was there four months ago.

But here's what changed for me: **I still do traditional hand-crafted coding in my day job. I regularly work through code katas, which are fun and enjoyable in and of themselves.** AI hasn't replaced my coding skills, it's multiplied what I can accomplish when I need to move fast or explore unfamiliar territory.

## Practical Workflows That Emerged

Through trial and error, I developed specific patterns to manage AI's weaknesses:

**1. The Planning Folder Pattern**
Keep numbered specs (1-initial-feature.md, 2-pay-by-discard.md, etc.) that document feature discussions. These become persistent context across sessions.

**2. The Todo Accountability System**
Break specs into granular checkbox lists. Use them to hold the AI accountable during implementation.

**3. The Git Save-Scumming Strategy**
Commit frequently. AI will overwrite working solutions without memory of what worked before.

**4. The Role-Based AI Selection**
- ChatGPT: Brainstorming, exploration, asking "what's wrong with this design?"
- Claude: Implementation, code review, pair programming
- Copilot/Codex: Ticket-style work where you hand off and come back later

**5. The Discipline Override**
Set hard rules to counter AI's momentum:
- Force refactor cycles
- Write tests even when AI makes it feel unnecessary
- Question every tangent: "Is this the MVP?"

## What About the Code Quality?

Let's be honest: the code AI generates can be good, can be overly verbose, tends toward duplication. But it can be nudged in the right direction quite easily.

The game currently works. It's not feature complete, not even a paired-down, super-trimmed version. But it's playable, testable, and iterating forward.

That's the trade-off: you get speed and momentum in exchange for code that needs shepherding. You're not writing every line, but you're still responsible for the architecture, the patterns, and the quality.

## Minimum Viable Prompt Literacy

I have no idea what a "perfect prompt" looks like. But I know one rule that consistently works:

**No matter what you ask the AI to make, the last sentence should be: "Ask me questions."**

Get the AI to ask *you* questions. Ask it "what am I missing?" type questions. This back-and-forth is where the real value emerges, not in the first response, but in the dialogue.

It took me 2-3 weeks to figure this out, but once I did, everything clicked.

## The Bottom Line

AI hasn't replaced my thinking, it's changed how I work. The best analogy I've found: it's like pairing with a junior engineer who:
- Never gets tired
- Has read everything
- Has no memory between sessions
- Will confidently suggest terrible ideas alongside brilliant ones
- Makes everything feel achievable (which is both blessing and curse)

You have to bring the discipline, direction, and judgment. The AI brings speed, exploration, and momentum.

After four months of solo exploration,watching YouTube videos, AI Engineer conference talks, and lots of trial and error,I'm not worried about my career ending. I'm worried about not learning these tools fast enough.

## Why This Matters (and Why I'm Writing This)

I'm writing this for two audiences:

**Future me**: So I can succinctly explain "this is what I learned" when the details fade.

**You**: To give you an idea of how to approach AI development that's more than the nebulous "what the hell do I do here" feeling I had in June.

This is an invitation. Not a tutorial, not a manifesto,an invitation to experiment, to treat side projects with these tools as "learn how to AI" projects, and to discover your own patterns through building.

Because here's what I know now: the developers who learn to work effectively with AI aren't going to replace the ones who don't. They're going to outpace them by an order of magnitude.

The question isn't "will AI take my job?" 

The question is: "Am I learning to multiply my effectiveness, or am I just playing with shiny tools?"

For me, the answer finally became clear somewhere between a Magic the Gathering cube and a procedurally generated sky island wargame.

I'm building the plane while flying it. And documenting the journey as I go.

Because maybe, just maybe, someone else is standing where I was in June, wondering "how does one actually vibe code?"

And maybe this helps them take the first step.
