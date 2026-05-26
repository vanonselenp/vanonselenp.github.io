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

{% assign halftruck_images = site.static_files | where_exp: "f", "f.path contains '/assets/doesnt-look-like-anything/halftruck/'" | sort: "name" %}
<div class="model-carousel" style="position: relative; width: 100%; max-width: 800px; margin: 1.5rem auto; text-align: center;">
  <div class="model-carousel-track" style="display: grid; border-radius: 4px; overflow: hidden;">
  {% for file in halftruck_images %}
    {% assign filename = file.path | split: "/" | last | remove_first: ".png" %}
    {% assign leading = filename | slice: 0, 1 %}
    {% assign label = filename | remove_first: leading | remove_first: "-" %}
    <img src="{{ file.path | relative_url }}" alt="Half-track — {{ label }}" data-label="{{ label }}" style="grid-area: 1 / 1; width: 100%; height: auto; opacity: {% if forloop.first %}1{% else %}0{% endif %}; transition: opacity 0.25s;" />
  {% endfor %}
  </div>
  <button type="button" class="model-prev" aria-label="Previous" style="position: absolute; top: 50%; left: 0.5rem; transform: translateY(-50%); background: rgba(0,0,0,0.55); color: #fff; border: 0; border-radius: 50%; width: 2.25rem; height: 2.25rem; font-size: 1.25rem; cursor: pointer;">‹</button>
  <button type="button" class="model-next" aria-label="Next" style="position: absolute; top: 50%; right: 0.5rem; transform: translateY(-50%); background: rgba(0,0,0,0.55); color: #fff; border: 0; border-radius: 50%; width: 2.25rem; height: 2.25rem; font-size: 1.25rem; cursor: pointer;">›</button>
  <div style="margin-top: 0.5rem; font-size: 0.9rem; color: #666;"><span class="model-label"></span> &middot; <span class="model-current">1</span> / {{ halftruck_images | size }}</div>
</div>
<script>
(function () {
  var root = document.currentScript.previousElementSibling;
  var imgs = root.querySelectorAll('.model-carousel-track img');
  var counter = root.querySelector('.model-current');
  var label = root.querySelector('.model-label');
  var i = 0;
  function show(n) {
    i = (n + imgs.length) % imgs.length;
    imgs.forEach(function (img, idx) { img.style.opacity = idx === i ? '1' : '0'; });
    counter.textContent = i + 1;
    label.textContent = imgs[i].dataset.label || '';
  }
  root.querySelector('.model-prev').addEventListener('click', function () { show(i - 1); });
  root.querySelector('.model-next').addEventListener('click', function () { show(i + 1); });
  show(0);
})();
</script>

Same input image. Four very different hosts running the same loop.

**Meshy 6** is the only one that understood the word *half-track*. Tracks at the back, wheels at the front, the whole silhouette correct. When Meshy hallucinates the bits it can't see directly in the input image, it hallucinates *in character*. It has a sense of what a WWII half-track is and fills in the missing parts with something consistent. Jerry cans, stowage, period-appropriate clutter. The back of the vehicle exists, and the back of the vehicle looks like it belongs to the front of the vehicle.

**Trellis** got the vehicle vibe right and then ruined the take on the cast. The body of the half-track is plausible, the crew are posed with intent, sitting properly in the troop compartment. But the heads are shaped strangely in a way that breaks the whole thing once you notice it. Composition right, anatomy off. It is doing something the others aren't, which is treating the scene as a scene rather than as an object plus passengers, and I want to like it more than I do.

**Rodin** is the most restrained of the four. Clean, symmetric, prescriptive. It feels less like a generated artefact and more like something that was already in the model's head and the input image just nudged it to commit. The crew look fine but feel imported from somewhere else. There is also a quiet warning underneath the render that the mesh has more than a million triangles and might be slow to slice, which is its own little tell about how Rodin approaches the problem.

**Hunyuan3d-2mv** is unrefined clay. The crew are oversized and cartoonish, the proportions of soldier-to-vehicle are off, and the whole thing has a roughed-in quality to it. You can see what it was reaching for. It just didn't get there.

The personalities are real, and they are persistent. Each model has a way of being wrong that is recognisable across outputs. Once you have seen enough of them you can almost name which model produced a render without checking.

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

