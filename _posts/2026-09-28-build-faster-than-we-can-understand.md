---
layout: post
title: "We Can Build Faster Than We Can Understand"
date: 2026-09-28 06:00:00 +0000
categories:  personal claudecode softwarecraftsmanship
image: /assets/build-faster-than-we-understand.png
thread: craft
tags: [ai-assisted-engineering]
---

*The Road to Hell Is Paved With Green Checks...*

---

![We Can Build Faster Than We Can Understand](/assets/build-faster-than-we-understand.png)

I started a new job recently, and the new place is fast. Night and day faster than anywhere I've ever worked. Everything is agentic, there's a review pipeline that runs a stack of checks on every PR, and the amount of change moving through in a day is more than one person is built to hold in their head. Each engineer is shipping dozens of PRs a week. There's a new bottleneck now. And for a while I assumed it was me.

Recently I picked up what looked like a simple permissions problem in one part of the product. Solve it, make it work, move on. I thought it needed an ethical wall. That's the hard barrier firms put up to keep one side of a deal from seeing the other: strict rules about who can see what, when, and whether it can ever be shared back. So I built one. The full thing. All the tracking, all the locking, a careful staged rollout, the whole kitchen sink. I got a working prototype through the automated review and sat there waiting to click merge.

It took a day. Anywhere else it would have taken two weeks or more. You'd whiteboard it, argue about it, get sign-off before anyone wrote a line. I stood it up in a day.

I've been experimenting with a review routine I run on every PR, mine and everyone else's. You can't read a few thousand lines of generated code line by line. You won't hold it in your mind. Nobody can. So instead I get a fresh agent to explain what changed. Then draw the architecture. Then show me the sequence diagrams. Then the call stack. Then tell me which files actually matter, and why. And then I go in and pick the thing apart against all of that. It's a good routine. It catches things nothing else does.

I ran it on my ethical wall. It told me it was well designed and solved the problem. The only problem was that it was the wrong problem.

The checks were green. The review agents were happy. It was clean, it was tested, it did exactly what I'd asked for. It was just the wrong solution, built very carefully. Nothing in the pipeline could tell me I'd asked for the wrong thing. It only clicked once I had the diagrams in front of me and could see what it actually did. The people this part of the product served weren't the ones who needed walls. They needed to share, not to be kept apart. I'd built a barrier for people whose whole problem was that they wanted to work together.

So I started fresh. Brand new checkout. Threw the whole thing away, kept what I'd learned.

The second attempt was wrong too, the other way. I overcorrected, locked it down too hard, gave everyone their own private space, and killed the one thing that made the feature worth having, which was people working together. So I binned it. Kept the learning. Started again on a new branch.

This time it landed, and it was almost embarrassing how small the answer was. It was never an ethical wall. It was never anything clever. It was a view permission. A bog-standard sharing problem. That's the whole thing. It just took two elaborate wrong answers to see it.

It would be nice to tell you I started over twice because I was deliberately spiking it out of discipline. I wasn't. I started over twice because I kept building the wrong thing, and only caught it because I insisted on understanding what each change was actually doing. That habit is the hero of this tale. Not me.

I could build the wrong thing all the way to done, twice, because each attempt only cost a day. When being wrong costs an agile team two weeks, the cost forces the argument early. Someone stands up before the work starts and asks who's actually going to use this. When being wrong costs a day, nobody asks. Cheap building didn't just make me faster. It took away the point where the cost used to force the right question.

But asking wouldn't have helped. Who these people were, what they needed and why, none of it existed as a settled fact in anyone's head. My three builds were spread across three weeks of meetings where everyone went away, thought about it, built a little more, and came back knowing a bit more than last time. We were shipping half a dozen PRs a day the whole time. There was never a point where I could ask the right question and get the right answer, because the answer was still being put together by a group of people, at the speed groups of people think.

I think this is the bottleneck. It wasn't me. It isn't building, which is nearly free now. It isn't even validating the code, which a good set of habits mostly handles. It's the slow thing. A group of people working out what they actually need a product to do, one decision at a time.

My problem is that every step of my routine happens after the agent builds. Explain what this changed. Draw the architecture it made. All past tense. I've built a genuinely good process and it's an autopsy from start to finish.

So the obvious next move is to change how I write my specs and drag it all upstream. Spike for knowledge first and be willing to delete sooner. Draw the diagrams before the build instead of after, and use them to hold the agent to account. I'm going to try it. It might be where the whole habit was always heading.

Except I've just spent three paragraphs arguing that you can't front-load an understanding the organisation hasn't finished making. And those wrong builds might have been part of how it got made. Moving the habit upstream won't make the answer arrive any sooner. The best I can hope for is that it lets me learn faster alongside everyone else, rather than ahead of them.

I don't know if this will work yet. I'm still figuring it out. One mistake at a time.