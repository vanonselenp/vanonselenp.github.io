---
layout: post
title: "I Actually Stayed On Task (For Once): A Dev Miracle"
date: 2025-10-24 08:00:00 +0000
categories: personal board-game godot video-game claudecode codex vibecoding
---

_Breaking news: Developer completes planned features ... who would have thought?_

---

Remember all those high-minded ideas I had about [staying on task with AI-assisted development](https://www.petervanonselen.com/2025/10/20/what-i-have-learnt/)? All that big game I've been talking about "this is how you do dev with an AI and keep it on task" and "this is the way you got to do it"? 

Yeah, about that.

If you've been reading the wonderful adventures of the tangent king over here, I know what you're thinking. He can't do that.

**For context:** I'm building Horizon's Edge: a turn-based tactical wargame inspired by NetStorm where floating islands battle for control of the skies. I've been developing it with AI assistance in Godot, and staying focused has been... a journey. Previous highlights include: diving into Wave Function Collapse procedural generation instead of finishing game rules, and a grand refactor that ate five entire evenings because I accidentally committed the `.godot` cache folder.

Well, I will have you know... that this week I set out to get a bunch of combat systems up and running. Working tip top. No funny business with wave function algorithms or hexes or anything! And I managed, for the first time in almost 4 months, to stay on task and not meander (too much) and actually get some things *completed*. 

![mage!](/assets/stay-on-target/mage.png)

I now have 3 creatures, each with at least 1 or more special abilities and those abilities actually work. I know! I am surprised too. I'm meandering my way through my todo list and this week I have a test mage with 5 abilities actually working:

- **Blink** - Teleportation ability
- **Ethereal Phase** - Phasing ability  
- **Arcane Missile** - Ranged magic projectile
- **Divination** - Detection/reveal ability
- **Mana Drain** - Resource manipulation ability

I might have wandered off and made one of the spells do terrain destruction too. Arcane Missile is the first ability in the game that actually destroys terrain rather than just building it. I just love the idea of the battlefield being dynamic and changing under the players' feet. Right now it wipes out the hex the target was standing on, plus a 50% chance on each of the 6 surrounding hexes. The idea is that if a creature is no longer standing on anything, even if it has a lot of health, it will plummet to its death. It should create tension around expansion and positioning. Do you risk getting close for that attack if one wrong spell could drop you into the void?

![Island destruction](/assets/stay-on-target/destruction.png)

I also figured out how to get rounds and turns working together (this was needed for Ethereal Phase). And I might have spent some silly time hacking in a few animations to make the effects a bit more obvious when they happen.

Admittedly none of this is "let other people play with it" yet. And it doesn't yet have a win condition. But it is meandering in a direction.

See? Like I told you. Todo list! Let's see if I can do it again?

**Next up on the todo list:** Three more creature archetypes, each with their own special abilities.

- `test_voltage_bot` with Overcharge and Turbo Boost abilities. 
- `test_biomass_spawn` with Regenerate and Spawn Swarmlings. 
- `test_flux_walker` with Chaos Bolt and Lucky Strike.

...assuming I don't get distracted tweaking that wave function collapse algorithm again.

![tangent king](/assets/stay-on-target/Distracted-Boyfriend.jpg)

**Incidentally, the stats for the week:**
- 32 files changed  
- 3,029 additions
- 508 deletions
- Net addition of ~2,500 lines of code

For an hour and a bit each night, the progress here is just down right fierce!
