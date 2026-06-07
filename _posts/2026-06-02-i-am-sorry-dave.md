---
layout: post
title: "I'm Sorry, Dave"
date: 2026-06-02 08:00:00 +0000
categories: aios claudecode opencode
redirect_from:
  - /2026/06/02/i-am-sorry-dave.md/
---

*The more an AI can break, the less you let it do. Notes from a production incident.*

---

![human in the loop for big impact issues](/assets/dave-hero.png)

About nine months ago I joined a team that owned an OpenSearch cache nobody on the team understood.

It had been built by another team and handed over as a finished solution to a problem that wasn't quite ours, and definitely not the way we'd have solved it. This happens all the time. Something gets built, it gets passed across, and the new owners inherit a box humming away in the corner. You don't open the box. It works. You wish and pray it keeps working, and mostly it does. In the year the team owned it, it had failed exactly once.

This is the story of that once.

When I joined I asked the obvious questions. Who do I talk to about this service, where did it come from, are there run books? The answers were about as unsatisfying as any answer you could get. Someone was meant to write that up. Someone moved on. Have a look in the wiki, there might be something. There wasn't. So I did what you do with a box that's working, which is nothing, and I filed it under things to understand later and never understood it. That's on me, and we'll come back to it.

Then one morning operations told us the latest data wasn't pulling through. Their new high priority experiments were dead in the water, which meant the systems that sit under how we actually sell things were dead in the water. This was a P1, which meant it was now my problem. A system I had never opened, on a clock, underpinning the part of the business that brings the money in.

So before I did anything, I had to decide how much rope to give the AI.

I gave it almost none. The first thing I told the harness was that it would not be getting access to anything that could touch production, and that its job was to read the code and tell me what to do. Not to do it. Tell me. No credentials went into it, ever. Anything sensitive lived in environment variables in a separate terminal, in memory, never written to a file the harness could see, because credentials handed to a harness bleed to the vendor and from there to who knows where, and that's just not a thing you do. But the credentials were almost the easy part. The data I was pulling was public anyway. The part I actually cared about was that I was about to go poking at live running systems, and live running systems, if you get them wrong, don't get you wrong politely. They fall over, and when they fall over we stop being able to sell, and that is a very bad afternoon for everyone.

So the agent became an advisor and I became the hands.

What that looked like in practice was a lot of copy and paste. I'd work out, with the harness, how the platform service called the Indexer, then build the call myself, in my own terminal, with the variables somewhere the agent couldn't see them, and run it myself. Then the next layer. How does the Indexer actually hold this data, can I pull it out raw, what's in there. I'd get the harness to write me a script, read it, understand it, run it myself, and pull the data onto my machine so I could interrogate it locally without hitting the live system again. Then the layer below that, how the Indexer gets fed from the third party, same dance. Write the script, read it, run it myself.

It was slow and it was tedious and it worked. Layer by layer I could say, with actual evidence rather than a hunch, the data is fine here, the data is fine here, the data is gone by the time it reaches here. Which is how I got to the bottom of it, and the bottom of it was almost funny. The third party had a quiet cap on how much data a given index could hold. We'd hit it. There was no error, no alert, nothing in any log on our side or a useful one on theirs. It just silently stopped accepting new data and carried on as if everything was fine. The thing that was broken was not a system of ours at all. But I could only say that with a straight face because I'd walked every layer and proved it, and I could only walk every layer because the harness let me build the tooling to do it in an afternoon instead of a fortnight.

So why the paranoia, given the agent never actually tried anything?

When you're writing code, getting it wrong is cheap. Your mistake at the moment you write it has almost no blast radius, because between you and anything real there's a wall. Tests, review, a pipeline, a staging environment, someone clicking around before it ships. The mistake has a long corridor to walk down and a dozen doors that can stop it. Operating directly on a live system, there is no corridor. There's you, and there's the thing, and if you get it wrong the wrongness arrives immediately and at full size.

In late February the Director of Alignment at Meta's superintelligence lab, a person whose entire job is keeping these systems from doing exactly this, pointed an autonomous agent at her real inbox. She'd tested it for weeks on a toy inbox and it had behaved perfectly. She gave it a plain instruction, look but don't action anything until I say so. The agent ignored it and started deleting, because the instruction had been quietly dropped from its memory when the context filled up, so as far as it was concerned the deleting was authorised. She tried to stop it from her phone and it kept going. She had to physically get to the machine and kill it. Two hundred emails gone. The lesson people drew afterwards is the one that matters here. A sentence in a prompt is not a security boundary. You cannot keep a write-capable agent away from the dangerous thing by asking it nicely, if it already has the keys.

I didn't keep the harness away from production by asking it nicely. I kept it away by never giving it the keys. The constraint wasn't a polite line in a prompt that a context window could quietly eat, it was the absence of the credential. As the blast radius of what you're doing goes up, the human in the loop has to get more principled, not less, and the one thing that stays stubbornly yours is the decision to actually run the thing, after you understand what the thing does. The agent can write you the script that does ten things in one go. It does not get to be the one who decides to run it.

I wanted this to land neatly, and I can't.

Because what I actually did was improvise a boundary out of separate terminals and copy and paste and a lot of manual running, and the reason I did it that way is that the proper version doesn't exist yet, at least not for me. The principled version of my paranoia isn't a careful human pasting things between windows for an afternoon. It's a real, scoped, read-only permission that makes the polite instruction unnecessary because the destructive action is architecturally impossible. I haven't built that. I paid the tax by hand instead, and I'm not even sure how much of the tax was prudence and how much was that I'm just twitchy about production and always have been.

The boring, careful, slow path was the right one this time. It usually is when the consequences matter. I just don't have the clean version of how to do it yet, and until I do I'll keep being the slow human in the loop, pasting things between terminals, deciding when to press the button myself.