---
layout: post
title: "AI Spec Driven Development"
date: 2025-10-30 08:00:00 +0000
categories: personal claudecode vibecoding
---

_A brief summary of what I have learnt_

---

This is an exert of [From AI Skeptic to Constant Collaborator: What I Learned Vibe Coding](https://www.petervanonselen.com/2025/10/20/what-i-have-learnt/). 

## Practical Workflows

Through trial and error, I developed specific patterns to manage AI's weaknesses:

**1. The Planning Folder Pattern**
Keep numbered specs (1-initial-feature.md, 2-pay-by-discard.md, etc.) that document feature discussions. These become persistent context across sessions.

**2. The Todo Accountability System**
Break specs into granular checkbox lists. Use them to hold the AI accountable during implementation.

**3. The Git Save-Scumming Strategy**
Commit frequently. AI will overwrite working solutions without memory of what worked before.

**4. The Role-Based AI Selection**
- ChatGPT: Brainstorming, exploration, asking "what's wrong with this design?"
- Claude: Implementation, code review, pair programming
- Copilot/Codex: Ticket-style work where you hand off and come back later

**5. The Discipline Override**
Set hard rules to counter AI's momentum:
- Force refactor cycles
- Write tests even when AI makes it feel unnecessary
- Question every tangent: "Is this the MVP?"

## Minimum Viable Prompt Literacy

I have no idea what a "perfect prompt" looks like. But I know one rule that consistently works:

**No matter what you ask the AI to make, the last sentence should be: "Ask me questions."**

Get the AI to ask *you* questions. Ask it "what am I missing?" type questions. This back-and-forth is where the real value emerges, not in the first response, but in the dialogue.
