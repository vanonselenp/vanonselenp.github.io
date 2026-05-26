---
layout: post
title: "Doesn't Look Like Anything to Me"
date: 2026-05-26 08:00:00 +0000
categories: aios claudecode opencode
---

*What happens when you point five 3D generation models at the same concept image.*

---

I have been generating 3D models of World War II miniatures for printing. Concept image in, printable model out, slice it, print it on an A1 mini. The 3D model generation has been mostly Meshy, because Meshy has been mostly good enough, and good enough is a powerful drug.

Then I ran out of credits.

Of course I did. The credits don't map to dollars in any way I can keep in my head. You get a monthly allocation on the sub, and you spend them in increments of "twenty credits for this thing, hopefully that means something useful at the end of it." Which is fine until the day it isn't, and the day it isn't is the day you have momentum and an idea and a queue of concept images lined up, and the tool politely tells "Your call is important to us ... please hold...".

So I went looking for an alternative. Found Replicate. Replicate hosts four or five different 3D generation models behind a single interface, which meant that for the first time I could give the same concept image to several different models and look at what came back.

Which meant the credit wall hadn't blocked me. It had just rerouted me into something much more interesting. An experiment!

## PrintBench CLI needed a tune up

The CLI I had built to drive all of this was vibe-coded. It talked to Meshy because Meshy was the thing that worked, and there was no reason to abstract anything until there was a reason to abstract something. Now there was a reason. I wanted to swap backends, and ideally I wanted to swap between multiple backends without thinking about it.

I used Matt Pocock's `improve-code-architecture` skill to walk through the refactor. The skill raised some potential wins, I went for the Adapter pattern because Science! The CLI now has a proper adapter interface. Meshy is one backend. Hi3D is another. Replicate is a third, and behind Replicate sit a handful of named models with their own adapters.

The current lineup:

- meshy
- hi3d
- hyper3d/rodin
- tencent/hunyuan3d-2mv
- tencent/hunyuan-3d-3.1
- fishwowater/trellis2
- prunaai/hunyuan3d-2
- firtoz/trellis

Which means I can give the same concept image to multiple models, line the outputs up next to each other, and look at how they each interpret the same brief.

## The half-track

{% include model-carousel.html path="/assets/doesnt-look-like-anything/halftruck/" alt_prefix="Half-track" %}

Same input image. Very different models as output.

## The jeep

[jeep comparison image — placeholder]

[per-model notes once renders are in. The thing I want to land here is how each model handles a vehicle that's all open structure, where there's nowhere to hide. The earlier observation about Hunyuan's *fairly reasonable guess* — the German half-track that looked great from the front, top, and sides and then turned into a block of mud at the back — is the punchline I'm circling. The model has nothing to work from for the back, so it gives up. Meshy on the same input puts jerry cans there, because Meshy is hallucinating in character.]

## The infantry

[infantry comparison image — placeholder]

[per-model notes once renders are in. The thing I want to land here is that infantry is where the ranking shifts. For vehicles I reach for Meshy every time because Meshy is willing to confabulate plausibly and the back of a half-track has to exist somehow. For infantry the bar is lower in some sense — a single figure, less hidden geometry, fewer places for a model to give up — and that means Hunyuan and the others become more viable. Which is useful, because it means I'm unblocked on infantry work even while still being constrained on vehicles.]

## What the experiment actually revealed

What started as a workaround for running out of Meshy credits has turned into something I find genuinely useful, which is a set of personality reads on five different 3D generation models. Meshy is still the one I reach for when I want a printable vehicle, because Meshy is willing to invent the parts it can't see in a way that fits with the parts it can. Hunyuan is honest about what it doesn't know, which is a trait I respect in a person and find frustrating in a generator. Trellis has compositional ambition that its execution can't quite cash. Rodin is restrained to a fault.

None of this was visible to me when I was just using Meshy. I had a tool that worked, and "works" is a state that hides everything about the shape of how it works. Putting five models behind one interface and pointing them at the same input is what made the differences legible.

The point I keep coming back to is that the refactor isn't the headline. The refactor is the thing that made the headline visible. The credit wall pushed me to Replicate, and Replicate gave me a reason to do the adapter work, and the adapter work gave me an experimentation engine I didn't know I was building.

I should probably hit credit walls more often.

