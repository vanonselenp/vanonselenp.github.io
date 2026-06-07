---
layout: post
title: "I Didn't Grok Superpowers"
date: 2026-05-23 08:00:00 +0000
categories: aios claudecode opencode softwarecraftsmanship
---

*You Can't Just Install Someone Else's Workflow and Level Up.*

---

![Not all skills will fit your way of working](/assets/i-didnt-grok-it.png)

The skills moment is happening. Matt Pocock's repo is blowing up. Superpowers, nwave.ai. Curated bundles of markdown being treated as installable expertise.

I've spent the last year holding back. Not because I think any of these are bad. Because I've been very consciously trying to learn the fundamentals first. How do I frame the question I'm asking. How do I prompt. How do I write a spec. How do I build the context I need to get meaningful results out of an agent. Working with AI harnesses forces a kind of explicitness that working alone never demanded of me. You can't be vague with an agent and get good results, so the vagueness gets cooked out of how you think. That's been the project. Iterating on the way I phrase things, the way I decompose problems, the order I bring context in, until the patterns started showing themselves.

Recently I have been feeling like it is time to start experimenting with skills.

I started with Obra's Superpowers...

And it made my experience significantly worse. Bad enough that I uninstalled it, purged the cache, and deleted it from every machine I could touch. Why this failed is particularly interesting. At work I spend a lot of time debugging things that cross multiple repositories, pulling in context from New Relic, GitHub, Atlassian and more, doing this rich synthetic conversation where I'm trying to _understand_ a problem before I do anything about it. With superpowers installed, the agent _kept_ trying to write documents. Reach for structured outputs. Produce artefacts. While I was still trying to investigate. It defaulted to choices I wouldn't have made and actively got in the way of what I was trying to do.

Superpowers isn't wrong about what it does. The outputs it produces are useful. Documents are useful. It's wrong about _when_, at least for me. It pulls the agent into ceremony during the part of the work that needs to stay loose. The exploration collapses into artifact-production before you've actually understood what you're looking at.

I didn't bounce off superpowers because it's a bad framework. From what I can see from the outside it is a great framework. I bounced off it because I didn't grok it. People are clearly getting real value out of these systems. My way of working with agents has been fundamentally different from how a lot of the loudest voices online are doing it, and that doesn't make either of us wrong. It just means borrowed intelligence doesn't transfer the way the marketing suggests. You can't take someone else's curated skills repo and have it magically make you think like them.

So I'm doing the opposite. Pull a single skill. Try it. Keep it if it fits, drop it if it doesn't. There are two from Matt Pocock that I am definitely keeping.

The first is `handover`. It's almost a one-to-one fit with something I was already doing manually. I spend a context window in one terminal getting a spec right, then feed that spec to another terminal or agent to implement. Handover formalises that pattern, doesn't litter the workspace with random files, and stays out of the way otherwise. It clicked instantly because it named a practice I already had.

The second is `improve-code-architecture`, and this one's more interesting. I tried it on a vibe-coded side project, a CLI that automates some of my 3D modelling work. The CLI had become a god file because the proof of concept had quietly become production code, as proofs of concept tend to do. The skill went through the code, surfaced its analysis as an HTML file, asked targeted questions to narrow down the right intervention, and then dropped back into normal conversation mode informed by what it had just produced. Analyse, surface a real artefact, return to conversation. The skill picks up structure briefly and then puts it back down. It doesn't replace the conversation, it _informs_ it. That's the opposite of what superpowers did to me.

What I think I've actually learned recently is that _skills are compressions of patterns_, and a compression is only useful at the point in your practice where you've learned enough pattern recognition to know which compressions are yours. Adopt them too early and you're running someone else's decomposition style on top of a workflow that doesn't share its shape, and the result is friction you can't quite name. Adopt them at the right moment and they feel like puzzle pieces. Same skill, same code, different person ready to receive it.

I didn't grok superpowers. That's okay. The point isn't that it's wrong. The point is that I needed to spend a while doing this the hard way before I had any business deciding which shortcuts were mine.
