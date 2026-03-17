---
layout: post
title: "The Feedback That Doesn't Care About Your Title"
date: 2026-03-17 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_What doesn't kill you makes you stronger ... right?_

---

I've been writing this blog for a while now. I've documented scope creep spirals, the joy of deleting code I spent weeks writing, and the slow painful education of learning to work with AI agents without letting them run off a cliff. If you've been following along, you know the theme by now: I learn things the hard way and then write about it so you don't have to. Or at least so you can watch.

Yesterday I was explaining to a colleague how I use Gemini to give me personalised feedback on my performance after meetings. He's a staff engineer, someone who's genuinely deep into AI-assisted coding, not a tourist. And even he stopped and went: "Wait, you're doing *what*?"

That reaction made me step back. Because I hadn't really sat down and thought about what I'd actually built over the past year. I'd been solving problems one at a time, better code generation here, better context gathering there, a way to get honest feedback on myself over here, and somewhere along the way it had become something bigger. A system. A layer underneath how I work that I now can't imagine working without.

So this is me trying to describe what that looks like, now that I've finally noticed it.

![the layers](/assets/feedback-that-kills-you/image.png)

## The code layer: get off the autocomplete

If you're writing code with an AI assistant inside your IDE, Copilot in VS Code for instance, I'd gently suggest you're missing the better experience. CLI agents like Claude Code, Codex CLI, and Open Code have fundamentally changed how I interact with code. Open Code has become my go-to because it works well straight out of the box and, crucially, it connects to Copilot's backend models. If your company already pays for Copilot, Open Code might be the unlock you didn't know you were waiting for.

The shift matters because it changes what the AI is doing. Inside an IDE, it's autocomplete with delusions of grandeur, guessing what you want line by line. On the command line, I'm describing problems, analysing architecture, pulling systems apart, generating diagrams. It stops being a typing assistant and starts being a thinking partner.

I use this for everything that touches code directly: writing it, reviewing it, debugging, breaking things apart to understand them, building architecture diagrams. The lot.

## The context layer: taming the organisational scatter

Every engineer in a large organisation knows this pain. The information you need to do your work lives in seven different places: Slack threads, Google Meet recordings, Confluence pages, Jira tickets, GitHub PRs, and at least two places nobody told you about. You spend half your time assembling a coherent picture before you can even start thinking.

ChatGPT and Claude's enterprise integrations have changed this for me. Both allow you to connect to corporate tools, your chat platform, docs, issue tracker, source control, and pull context into a single conversation. Instead of trawling through three Slack channels and two Confluence pages for forty minutes, I pull it all together and ask: what does this ticket actually need? What are the acceptance criteria? What am I missing?

Here's where it compounds. Good acceptance criteria from this layer mean better prompts for the coding agents. The layers feed each other. I didn't design it that way, it just happened once the pieces were in place.

## The mirror: feedback that doesn't care about your feelings

This is the hard one to talk about. And the one that made my colleague stop in his tracks.

We're a remote organisation. Google Meet is where everything happens, and Gemini sits inside every meeting. Most people don't turn on transcriptions, which I think is a mistake. Any meeting producing collective knowledge should generate a transcript. Those transcripts feed the context layer above.

But there's another use that took me months to work up to.

After meetings where I'm an active participant, I ask Gemini: as a staff engineer, what went well, what didn't go well, and what can I improve on?

The first few times, it was rough.

Here's the thing about feedback from humans: you almost never get anything useful. You either get "yeah, that was fine" or something so carefully hedged that whatever kernel of truth was in there has been sanded down to nothing. I've rarely received feedback that was specific, actionable, and tied directly to something I actually did in a real moment.

Gemini doesn't do hedging. It references specific things that happened in the meeting. "You reframed the argument here and it shifted the conversation constructively." Or: "You weren't listening here and this is where it cost you." It once told me that while I'd handled a frustrated colleague well, I could have spotted the frustration earlier and intervened before it escalated, and that when another colleague was dismissive, I'd recovered well but could have prepared for that reaction. Specific. Contextual. Minutes after it happened.

When I explained this to my colleague yesterday, he asked: "Isn't this just seeking perfection?" And I realised, no. It's just a way to learn and grow and become more deliberate about how I communicate, how I lead, and how I interact with the people around me. You can't improve what you don't measure. This is measuring.

But here's what really made me think this is bigger than my own little experiment. I told a principal engineer friend at another company about this approach. He had a difficult conversation coming up, recorded it with Gemini, and afterwards used the transcript to get actionable feedback on how he'd handled it. His reaction was genuine shock. He'd never had that clear a picture of how his conduct was landing. An engineering manager I know has started doing the same thing and describes it as brutal but the most meaningful feedback he's received in years.

And I think there's a reason for that. I remember chatting with a startup CEO at a meetup who made the observation that the higher you go in leadership, the less honest feedback you receive. The position of power makes it hard for people to cross that barrier. Gemini doesn't have any concept of your title or your seniority. It just tells you what it saw.

In the beginning, every session felt like a wake-up call. After months of doing this consistently, keeping a log, reading it back, it softened. Not because the feedback got less honest, but because the gap between what I thought I was doing and what I was actually doing got narrower. Fewer surprises. More gentle nudges, fewer gut punches.

## So what is this, actually?

None of these tools alone would be worth a blog post. A CLI coding agent is nice. Enterprise AI integrations save time. AI self-reflection is powerful but weird. What caught me off guard, what I only noticed yesterday when I saw my colleague's reaction, is that they work as a system.

Meeting transcripts feed the context layer. The context layer produces better acceptance criteria. Better acceptance criteria drive better output from the coding agents. The self-improvement loop makes me more effective in the meetings that generate the transcripts. Each layer feeds the others. I didn't plan it. I just kept solving problems and the connections emerged.

There's a Sam Altman interview from about a year ago where he describes people using AI as "an operating system for how they think." At the time I had absolutely no idea what he meant. Now I think I do, and the uncomfortable truth is that I'm probably barely scratching the surface of where this goes.

I'm still figuring it out. As usual, you'll hear about it when I do.