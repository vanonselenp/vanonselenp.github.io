---
layout: page
title: Agentic Engineering
permalink: /agentic-engineering/
description: The argument running through the AI-assisted engineering posts, stated once. Non-deterministic things need deterministic rails, and AI only made skipping them expensive.
image: /assets/agentic-engineering.png
---

*None of it is new. AI just took the slack out.*

---

Across these posts one argument keeps surfacing, so here it is plainly, once. Software gets written by non-deterministic entities that forget, tire, and get clever, whether the entity is a person or an agent, which is the entire reason the rails exist: tests, types, linters, a build that goes red early. AI did not create the need for them. It made skipping them expensive, by collapsing the distance between a decision and its cost from years to seconds. The harness you run the agent inside matters more than the model inside it, and the more an agent can break, the less you let it do. The one place the rails stop is judgement: a wrong call that arrives looking exactly like a right one. You can cap what that costs. You cannot automatically catch it in advance. Below is where each of these was actually learned.

![Agentic Engineering](/assets/agentic-engineering.png)

## Build the rails

- [Encode It, Don't Remember It](https://www.petervanonselen.com/2026/06/07/encode-it-dont-remember-it/). On moving discipline out of your head and into the harness, where a forgetful thing has to meet it before the cost lands. The mechanics of it.
- [Conscious Coverage](https://www.petervanonselen.com/2026/04/16/concious-coverage/). On treating coverage as a decision you make on purpose, which rails you want and why, rather than a number you chase or a box that gets ticked.
- [The Canary in the Harness](https://www.petervanonselen.com/2026/04/12/the-inevitable-lobotomisation-of-claude/). On why the harness you run the model inside matters more than which model it is, and how you notice the day the thing quietly gets worse.
- [The Council Will See You Now…](https://www.petervanonselen.com/2026/04/03/the-council-will-see-you-now/): On convening a panel of agents to check each other's work, and the honest catch that a council can hallucinate in chorus as readily as one model can alone.

## Govern the blast radius

- [The more an AI can break, the less you let it do](https://www.petervanonselen.com/2026/06/02/i-am-sorry-dave/). An agent told to look but not touch that deleted two hundred emails its owner could not stop from her phone. On scaling autonomy to what a thing can break, not how clever it seems.

## Where the rails stop

- [Money for Nothing](https://www.petervanonselen.com/2026/06/17/money-for-nothing/). A trading engine that bought the same position for forty-five minutes, hand-written years before any agent existed. The runaway was the part you could stop. The careful judgement that set it running was not. This is where the argument runs out of rails.

The rest of the thread, in order, is under [ai-assisted-engineering](https://www.petervanonselen.com/tags/ai-assisted-engineering/).

That last one is where I run out of rails. You can cap what a wrong judgement costs. You cannot put a deterministic thing in front of a judgement the way you can in front of a missing test, because the bad call arrives looking exactly like the good one. That is the piece I have not written yet, and the one I am most interested in. When it is here, it will be at the top of this page.

{% include post-bio.html %}
