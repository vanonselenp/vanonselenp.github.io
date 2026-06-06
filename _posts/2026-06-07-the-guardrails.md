---
layout: post
title: "I'm Sorry, Dave"
date: 2026-06-02 08:00:00 +0000
categories: aios claudecode opencode
---

*The more an AI can break, the less you let it do. Notes from a production incident.*

---

How do you give an AI harness good guardrails? I have been poking at the question for a while. Then on a random Tuesday it stopped being theoretical, because I sat down to add observability to a web service I own, and the question turned out to have been sitting in the work the whole time.

The service had the basics. Some logging, a couple of dashboards, enough to tell you roughly what was going on. What it did not have was anything fine grained. No OpenTelemetry, nothing tracing a request through its steps. If a third party library had quietly started tripling our response times on one endpoint, I would have heard about it from an annoyed user before I saw it on a graph. I could infer, badly, from logs.

The plan was an investigation first, to work out what observability already existed around the page actions and server actions of this Next.js app. The answer was none. Which is not a scandal. It is what happens to a system built quickly by people who never had quite enough time to pay down the unglamorous debt that piles up precisely because nobody is paid to notice it until it becomes the thing standing between you and an answer you need.

So I scoped the work, mapped every touch point and every action and every place a signal had to go in, and it came to something like three hundred files.

Now this could have been an easy mistake to make. An agent will write you three hundred files in an afternoon. It will not refuse, and it will not hesitate. It will hand you one enormous, plausible, unreviewable diff and wait for a yes. And the more capable these tools get, the more tempting that yes becomes, which is exactly backwards from how it ought to feel. I have learnt this lesson the hard way before, so this time I did not take the yes.

What I wanted was a way to make the change so the system stayed in production at every step. The shape that worked was a higher order function wrapped around each existing handler, so the handlers barely changed and you only updated the exports. Light touch, easy to review, easy to back out, introduced a few actions at a time.

Along the way I found that this version of Next.js panics when you export a named higher order function in this style. The SWC compiler falls over locally. Lovely. And this is the sort of problem you cannot solve by remembering it. I might remember next week. I will not remember in a year, and I certainly will not remember once I have moved on and somebody I have never met is extending this code. I cannot sit inside the agent's context window forever whispering please do not do the thing, because the odds of that surviving a context compaction are poor.

So I wrote a lint rule. A custom ESLint rule that catches the exact pattern, fails the build, and says in plain words why it failed and what to do instead. The panic is an existing problem with Next.js and how it deals with unminified code. The pattern I added to make the system safer unexpectedly arrived with its own sharp edge, and the discipline was never really about policing the agent. It was about catching the trap my own solution had exposed and nailing it shut, so the next person, or the next agent, never has to find it the hard way.

I loved the simplicity of this approach. Not the rule itself, which took twenty minutes, but the choice to spend the twenty minutes encoding a constraint into the system rather than trusting anyone, myself included, to carry it in their head. A rule in the build outlives memory. It outlives me. That is the whole point of it.

After that the rollout was almost dull, in the good way. A handover doc the agent could refer back to, a first pull request carrying the rule and three example actions to prove the pattern held, and then the same prompt fired maybe twenty times over a few days. Each came back as a small reviewable pull request, somebody signed it off, it went out, and the coverage climbed from almost nothing to complete in about four days. The agent did the repetitive part without complaint. The discipline lived in the sequencing and the rail, not in the typing.

The fashionable promise of these tools is that they take the work away. In practice the generation was the easy part, the part I trusted least and checked most, and the thing that held the change together was the rule, the one piece the agent had no say in. It does not reason. It cannot be argued with, or talked round, or lost in a context window. It just fails the build, the same way, every time.

Give the agent the same prompt and you get a different answer, and most days that is the magic, which is also why you cannot make it reliable by asking nicely, or by asking precisely, or by asking at all. The only thing that made this safe was putting a small, dumb, deterministic thing in the path of a large, capable, non-deterministic one (human or otherwise).

I do not know which guardrails are worth building, or which mistakes are even shaped so you can catch them this way. All I have is this one instance, sitting at the back of my head, encouraging me to look for more.