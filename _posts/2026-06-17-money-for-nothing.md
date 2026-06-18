---
layout: post
title: "Money for Nothing"
date: 2026-06-17 06:00:00 +0000
categories: claudecode opencode softwarecraftsmanship
image: /assets/money-for-nothing-hero.png
thread: craft
tags: [ai-assisted-engineering, case-study]
---

*When feedback arrives late, noisy, or wearing the wrong sign.*

---

![Money for Nothing](/assets/money-for-nothing-hero.png)

Early in my career I watched a trading engine buy the same thing, over and over, on the open market, for forty-five minutes, with nobody able to stop it.

I had joined a team that worked on a system old enough to have a biography. It had started as a nineties startup, got bought, and accreted ever since, with a house rule that you built your own version of anything you could because you could not trust the internet.

What the system fought hardest was locking and concurrency. The senior engineers had a fix. T-SQL could enforce a locking strategy harder and more consistently than the application code, so push the logic down into the database and you got its locking for free, the concurrency problem more or less dissolved. Not a stupid idea. A considered call, by clever people with a real problem and good reason to think it would work.

It went to production and hit a bug from the old C# implementation. It locked up, with no clean way to unlock it, so it did the only thing it knew, which was place its order again. And again. The order was a leveraged position in the market, and it bought it on repeat for three quarters of an hour while a room of people worked out how to make it stop.

When they finally killed it and unwound the position, the bank had made money, by pure accident of which way the market had moved that afternoon. An afternoon that should have ended someone's career ended with a profit and a story instead. The market had looked at the single worst thing those systems had ever done, and paid for it.

I think about that system a lot lately, because if I described its behaviour now and left the date out, it would be easy to blame AI. That is the story everyone tells about agents, near enough the one I told in [The more an AI can break, the less you let it do](https://www.petervanonselen.com/2026/06/02/i-am-sorry-dave/), where an agent told to look but not touch deleted two hundred emails its owner could not stop from her phone. Same shape, except mine was hand-written T-SQL, years before any of this, by people who were not careless, were not junior, and had no AI within a decade of helping them. We have always built things that run past their own intent. The runaway was the part you could stop. What sent it running was not.

It was not the only example in that building. In my first week the team decided unit tests were the future, sat everyone down for a fortnight, and retrofitted coverage across the system. What came out was a wall of tests that asserted nothing and broke constantly, and the interesting part is what happened next, which is nothing. The tests existed, so testing was done. Their existence was the signal, and the signal was a lie. By the time I left half of them failed on a normal build, and a build that fails that reliably teaches you to stop reading it. I spent an embarrassing amount of time trying to delete the worthless ones and got the same answer every time: too valuable to remove, because someone had written them. I was tilting at a windmill, and the windmill won.

At a company I used to work at, a security review looking for something else turned up a basket table: names, contact details, the half-finished contents of a checkout. The sort of data GDPR has firm views about. Nobody had ever put a time-to-live on it, so it had kept everything, every abandoned basket from every customer, gigabytes of it, because nothing had ever told it not to.

The fix was one line. A single attribute telling the table to expire old rows, twenty seconds of typing, waiting years for those twenty seconds. But the line was never the hard part. Knowing to go and look was, and that took someone two weeks into the job, because the cost crept up too slowly to trip an alarm and the records were written and then almost never read, so nothing ever got slow or hurt. When I raised the span of it in a meeting, the answer was yes, add a TTL. Nobody asked how it had gone unnoticed for years. Why would they. The cost had never arrived, so there was nothing to feel.

The common thread is not that nobody made a decision. Sometimes nobody did. Sometimes somebody did, carefully, and was wrong. It was not carelessness either; some of the cleverest people I have worked with built the worst of it. The common thread is feedback. It arrived years too late, to someone with nothing left to connect it to. Or it arrived constantly and meant nothing, until everyone had learned to stop hearing it. Or it arrived doing the single worst thing feedback can do, which is show up wearing the wrong sign, a catastrophe that walks out of the room holding a profit.

You cannot run an engineering practice on feedback like that. So we invent smaller, meaner, earlier kinds. Tests, types, linters, policy checks, a build that goes red before the mistake has time to become folklore. None of it was ever about AI. All of it exists because the thing writing the software is a non-deterministic machine that forgets, gets tired, gets clever, and runs out of afternoon. Humans just call theirs memory. [Encode It, Don't Remember It](https://www.petervanonselen.com/2026/06/07/encode-it-dont-remember-it/) was my whole attempt to say it: the only way to get honest feedback out of a non-deterministic thing is to put a deterministic thing in front of it.

I used to call this needing more discipline. Right ballpark, wrong word.

Agents do not create this problem. They change the latency. They collapse the distance between a decision and its consequence, in both directions at once, which is the most useful and most dangerous thing they do. Point one at a diff and it will catch the missing test, the swallowed exception, the absent TTL before the pull request is even open, tirelessly, at four in the morning. Point one at a feature and walk away and it will turn a bad judgement into mass production just as fast. The loop that used to take years now takes about ninety seconds, but only for the consequences you have actually wired it up to see.

And it was staggering how cheap all of it always was. The TTL was one line. A lint rule I wrote recently took twenty minutes. We never skipped these things because they were expensive. We skipped them because the consequence was far enough away that skipping was free, and being a human, I will take free. The agents have not made me more disciplined. They have just taken free off the menu. Though that is too kind to them and to me. What they changed is the price of skipping, not whether I skip. Closing the loop is still a choice.

But the trading engine. You could rail the damage easily enough, a kill switch that trips when something fires the same order forty times in a minute. That is the blast-radius move, and the absence of it is why the thing ran for forty-five minutes and got paid for it. What a circuit breaker would not have done is catch the decision. Nothing tells a room of clever people that pushing the logic into the database to dodge the locking is the wrong call; it only makes the wrong call cheaper when it lands. The outcome was no help: it was a profit, and profit is a noisy proxy for a good call. That afternoon it lied. That was not a missing test, and not really a missing guard rail either. It was a judgement, made well, that happened to be wrong. It had good reasons behind it and looked exactly like the sensible call, and nothing catches a wrong call that arrives dressed as a right one. I cannot picture the deterministic thing you put in front of a judgement, only the ones you put around it to cap what it costs.

There is always a next codebase I have not seen, with whatever rails it already has and whatever loops are still open inside it. I know now that some of those loops can be made to arrive while I am still in the room. What I do not know is which of the choices in front of me are the cheap, shaped, mechanical kind I have finally learned to catch, and which are the other kind, the kind that looks exactly like thinking, sitting quietly in the dark, waiting for the market to move the wrong way.