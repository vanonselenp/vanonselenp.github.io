---
layout: post
title: "Encode It, Don't Remember It"
date: 2026-06-07 06:00:00 +0000
categories: aios claudecode opencode softwarecraftsmanship
image: /assets/encode-it-hero.png
thread: craft
tags: [ai-assisted-engineering]
---

*Panic! at the SWC Compiler: cannot add pure comment to zero position.*

---

![reject the wrong pattern](/assets/encode-it-hero.png)

How do you give an AI harness good guardrails? I have been poking at the question for a while. Then on a random Tuesday it stopped being theoretical, because I sat down to add observability to a web service I own.

The service had the basics. Some logging, a couple of dashboards, enough to tell you roughly what was going on. Nothing fine grained. No OpenTelemetry, nothing tracing a request through its steps. I could infer, badly, from logs.

I started by working out what observability already existed around the page actions and server actions of this Next.js app. The answer was none. Which is not a scandal. It is what happens to a system built quickly by people who never had quite enough time to pay down the unglamorous debt nobody is paid to notice until it is the thing between you and an answer you need.

So I scoped the work, mapped every action and every place a signal had to go in, and it came to something like three hundred files.

Now this could have been an easy mistake to make. An agent will write you three hundred files in an afternoon. It will hand you one enormous, plausible, unreviewable diff and wait for a yes. And the more capable these tools get, the more tempting that yes becomes, which is exactly backwards from how it ought to feel. I have learnt this lesson the hard way before, so this time I did not take the yes.

What I wanted was a way to make the change while the system stayed in production at every step. The shape that worked was a higher order function wrapped around each existing handler, so the handlers barely changed and you only updated the exports. Light touch, easy to review, easy to back out.

Along the way I found that this version of Next.js panics on a particular shape. Wrap the handler, assign it to a local const, then export that const on its own line:

```ts
const sendInvite = withObservability('send-invite', sendInviteHandler, { /* ... */ });
export default sendInvite;
```

and the SWC compiler falls over locally with `cannot add pure comment to zero position`. Lovely. Inline that same call straight into the export and it builds fine. The handler does not change, only the shape of the export does, and that is the whole difference between a clean build and a panic. This is the sort of problem you cannot solve by remembering it. I will not remember in a year, and I certainly will not remember once I have moved on and somebody I have never met is extending this code. I cannot sit inside the agent's context window forever whispering please do not do the thing.

So I wrote a lint rule. A custom ESLint rule that finds that exact shape, fails the build, and prints the reason at the point it breaks:

```
withObservability(...) must be called directly as the initialiser of an
export default or export const statement, not assigned to a local binding
and re-exported. This avoids an SWC client-reference panic when the action
is imported from a Client Component.
```

The panic is an existing problem with Next.js. The pattern I added to make the system safer arrived with its own sharp edge, and the discipline was never really about policing the agent. It was about catching the trap my own solution had exposed and nailing it shut, so the next person, or the next agent, never has to find it the hard way.

What I loved was not the rule itself, which took twenty minutes, but the choice to spend the twenty minutes encoding a constraint rather than trusting anyone, myself included, to carry it in their head. A rule in the build outlives memory. It outlives me. That is the whole point of it.

After that the rollout was almost dull, in the good way. Before firing anything I wrote a plan that pre-decided one action per pull request, fixed the conventions once, gave the agent a short checklist to work through the same way each time, and ordered the runs so two of them never touched the same file at once. The awkward cases, the action that called another and double-counted a metric, the one that returned a failure instead of throwing it, were answered in the plan before the agent could reach them and guess. Then the same prompt fired maybe twenty times over a few days. Each came back as a small reviewable pull request, got signed off, and the coverage climbed from almost nothing to complete in about four days. The discipline lived in the plan and the rail, not in the typing.

The prompt was never written down. The plan lived in my checkout and never needed to be committed, because once the rollout was finished it had nothing left to do. The rule is the only part of any of this still in the codebase. It is the only part whose job does not end.

The fashionable promise of these tools is that they take the work away. In practice the generation was the easy part, the part I trusted least and checked most, and the thing that held the change together was the rule, the one piece the agent had no say in. It does not reason. It cannot be argued with, or talked round, or lost in a context window. It just fails the build, the same way, every time.

Give the agent the same prompt and you get a different answer, and most days that is the magic, which is also why you cannot make it reliable by asking nicely, or by asking precisely, or by asking at all. The only thing that made this safe was putting a small, dumb, deterministic thing in the path of a large, capable, non-deterministic one.

None of which is new. We have always known that people forget, that they do a thing one way on a Tuesday and another way a year later. Tests, types, linters, the build going red on a Friday afternoon, all of it exists because a human is a non-deterministic agent too, and always has been. The agent did not teach me anything I did not already know. It generated the change cheaply enough, and often enough, that I finally ran out of excuses for not encoding the discipline I should have encoded years ago. The lesson was never about the AI. The AI only made the right thing cheap, and the wrong thing harder to keep getting away with.

I still do not know which guardrails are worth building, or which mistakes are even shaped so you can catch them this way. All I have is this one instance, sitting at the back of my head, encouraging me to look for more.

---

**Related reading:** [Money for Nothing](/2026/06/17/money-for-nothing/) — on feedback that arrives late, noisy, or wearing the wrong sign.