---
layout: post
title: "I Built This In A Prompt Window! With A Box Of Filament!"
date: 2026-04-22 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_I Vibe Coded A Model Into My House_

---

There is a 3D printed World War II German infantryman sitting on my desk. He is about the size of my thumb, slightly chibi in the proportions, with a helmet a touch too large for his head. He looks, frankly, adorable. _He is also not a copy of anything_. Nobody designed him. Nobody sculpted him. Nobody even sketched him. I typed some words at a screen, pressed a button on a different screen, and twenty minutes later he was sitting on my desk. On the left pure vibes, on the right reality.

![hero](/assets/reality/hero.jpg)

I have been writing this blog for a while now about adventures in applying AI to dev related problems. Writing code. Building software. Making things. It has taken me through a Magic jumpstart cube generated with code, a board game prototype, a re-implementation of that prototype in Godot, a stealth tactics turn based game also in Godot, a news digest SaaS that is still somewhere in the middle of becoming itself, and a frankly embarrassing pile of bash scripts accumulated from deep dives into my coding harnesses. Along the way I have taken what I have learned and applied it at work. It has been a wonderful, bizarre road.

This post is about atoms instead of bits, which is a first for the blog. I promise it rhymes.

## The printer

Somebody gave me a 3D printer. An A1 Mini, which is one of the cheaper ones but turns out to be remarkably capable for what it is. And as one does when one acquires a 3D printer, I immediately spent a week not printing anything interesting. I built shelves for my office to create space. I printed spool holders for the spools. I printed the tools you need to use the 3D printer. This seems to be the compulsory onboarding ritual when you get a 3D printer, which is a bit like spending your first week with a new laptop installing a package manager so you can install the package managers that let you install things. Fine. Tradition.

Then I set myself an actual goal.

## The weird hobby compulsion

I should explain that I have a tendency to go on strange game-making tangents. I have built a travel sized version of a board game from scratch with custom cards and components, purely because it was fun to tinker with. I have made print and play versions of expansions for games I already own. I made my own version of Santorini using tiles and spray paint, like some sort of deranged hobbyist. I paint, I draw, I mess about. The point is that "I wonder if I could just make this" is my default failure mode when I encounter any game that costs too much or takes up too much space.

Bolt Action has been living rent free in the back of my head for two or three years now. It is a tabletop wargame. I would like to play it. But I do not want to spend the money on the models, I do not want to find the table space, I do not know enough people in my area who want to play it with me, and painting a hundred models is a lot of effort in a way that is genuinely hard to appreciate until you have sat there and done it.

The idea that has been sitting in the back of my brain for a few years is this: make a scale down version. Instead of moving in inches, move in centimetres. Same rules, same ratios, everything else the same, just smaller. Smaller table. Smaller models. Smaller paint commitment.

Which means you need smaller models. Which has always been the problem.

## The accidental pipeline

I saw a [blog post a while back by a guy making models out of Fimo clay and EVA foam and little bits of wood](https://talesfromfarpoint.blogspot.com/2026/03/junker-update-and-tiny-troops-how-to.html?m=1). They were cute and chibi and slightly weird and I really liked them. So naturally I tried to make one myself. What I ended up with functionally looked okay and matched the vibe but was basically 28mm scale, which is normal Bolt Action size, which defeats the entire point.

On a whim, I took the photo the original guy had taken of his model and fed it into Gemini Pro. "This style. World War II Germans."

![all](/assets/reality/all.jpg)

Gemini came back with something that looked astonishingly good. Cute, chibi, right proportions, right register. Something that immediately felt like what I had been trying to describe for years without quite having the vocabulary for it. I then started giving it more structured prompts. Give me a commanding officer. Give me an NCO. Give me a machine gunner.

![Meshy produced a 3D model](/assets/reality/meshy.jpg)

I took one of these entirely hallucinated images, cropped it, and fed it into Meshy, which is a generative tool that takes an image and produces a 3D model.

I then, mostly out of morbid curiosity, copied the file over to the printer and clicked print.

![hot off the print bead](/assets/reality/first.jpg)

## This confounds me

Twenty minutes later, there was a physical object on my desk. A German infantryman. About the size of my thumb. Cute and chibi, helmet slightly too large. Precisely the thing I had been describing to Gemini about half an hour earlier.

I want to be clear about what happened here because I think I am still processing it.

I described a thing in words. Another thing dreamed up a picture of that thing, a picture that had never previously existed. A third thing hallucinated a 3D shape from that picture, a shape that had also never previously existed. A fourth thing turned that shape into an object I can hold in my hand. No human sculpted it. No human modelled it. No human even sketched it. The infantryman on my desk has no reference in the world. He is not a copy of anything. He is purely the output of a *pipeline of vibes*.

*I vibe coded a model into my house*.

I have spent a year now playing around with generative AI. I have been, at times, out on what I thought was the frontier of what it is doing. I should have seen this coming. At some level I had seen this coming, in the abstract, "yes of course generative AI plus 3D printing, that is obviously a thing" way. But there is a chasm between knowing a thing is possible and holding the output of that thing in your hand twenty minutes after describing it out loud.

This is the same loop I have been running on software for a year. Describe a thing, get a thing, iterate, ship. The loop works on atoms now. It has probably been working on atoms for a while and I simply had not wired up the last step of the pipeline in my own life until somebody gave me a printer.

Which makes me wonder what else is already sitting there, loop closed, waiting for me to notice.

## What I'm doing with it

I am now in the middle of printing a 500 point German army and a 500 point Soviet army. The whole thing will probably fit in a box slightly bigger than a paperback. A deck of cards each for the rules and unit references. Total cost of the models, given that I already had the printer and the filament: functionally nothing. If a friend wanted to play, I could just print them a second army and not be fussed about it. There is some manual work around trimming supports and cleaning up sprues, but it is not the kind of work that scales with ambition. It scales with how many figures you feel like cleaning up on a given evening.

Something I have been idly wanting for two or three years is just there now, in a box, because the pipeline finally closed.

![current printed](/assets/reality/current.jpg)

## What I can't get out of my mind

Here is the thing that has been rattling around my head since the infantryman showed up.

We are, collectively, still arguing about whether vibe coded software counts as real engineering. That argument is live. It is on my timeline every week. It is in the comments of every post I write. People who build things for a living are genuinely unsure whether the loop of "describe a thing, get a thing, ship it" is a legitimate way to make software, and reasonable people disagree about that, and the discourse is maybe a year behind the tools and possibly more.

While we have been having that argument, the same loop has quietly grown another output head. It makes physical objects now. Not in some research lab, not in some well funded startup I would need to buy into. In my house, on a desk, using tools that anyone can download or buy, for a material cost measured in pennies per figure.

I found this out by accident. Someone gave me a printer. I had an itch I had been scratching at for years, and the pipeline closed on its own while I was not really paying attention. That is what is unsettling me. Not that it works. I knew it would work. It is that I walked into this corner of it entirely by accident, with no plan, and the corner was just sitting there waiting for anyone who happened to wander in.

I do not think we are ready for the software version of this. I am much less sure about anything else. Because if a ten minute detour into a completely different hobby is enough to produce an object with no human author, what else is already sitting there that I have not stumbled into? What other loops have quietly closed while I was looking at my terminal? I thought I had been playing on the frontier for a year. It turns out I have been playing in one room of a house whose floor plan I do not have.

I do not have a tidy ending for this. I have an infantryman on my desk, and a suspicion that I have been looking at a very small corner of something, and that almost everyone I know has been looking at the same small corner, and that the rest of the house is already built.