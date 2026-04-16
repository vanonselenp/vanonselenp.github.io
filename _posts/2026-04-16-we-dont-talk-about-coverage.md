---
layout: post
title: "We don't talk about Code Coverage"
date: 2026-04-16 08:00:00 +0000
categories: aios claudecode softwarecraftsmanship
---

_On discovering that your favourite tool got measurably worse, that you'd been blaming yourself for it, and that the only reason you noticed at all was because another harness was sitting right next to it behaving normally._

---

When I joined Cazoo, it was the first place I’d ever worked that explicitly, actively, aggressively embraced software craftsmanship. Pair programming. Test-driven development. Domain-driven design. Extreme programming. The whole kitchen sink. They sent us on agile training courses that a startup founder would weep at the cost of. We had an agile coach in the room every day. We did code katas regularly.

And even there, in the most craft-soaked environment I’d ever been in, the idea of 100% code coverage was treated as obvious lunacy. A poor metric. The kind of thing only someone who hadn’t really understood testing would chase.

Then I joined the Economist, and the team I landed on had 100% coverage as a hard rule.

They didn’t do TDD. They didn’t pair. They hadn’t been on the agile bootcamps. They hadn’t done code retreats or code katas. By every measure of either the London or Chicago school of craftsmanship tradition would care about, they were doing less of the work. But they had the 100% rule, and they enforced it, and at first I assumed they’d inherited a metric without fully understanding it.

They hadn’t. Turns out I hadn't understood it. And by the time I left that team, I’d come around entirely. Not reluctantly, not with caveats, but genuinely: 100% coverage, properly understood, is mandatory. I held that position for years before agentic coding was a thing anyone was thinking about. The agents haven’t changed my mind. They’ve just taken a position I already held and made the case for it screamingly, urgently obvious in a way it previously wasn’t.

## What is this metric thing about anyway?

Here’s what I’d absorbed from the craft world about 100% coverage. It’s a vanity number. Chasing it produces garbage tests. You end up writing assertions against getters and setters. You exercise code without testing behaviour. The pragmatic position, and pragmatism was always the emphasis, is that you write the tests that matter and you let the rest go.

All of that is true if “100% coverage” means “every line has a test exercising it.” That version of the metric is genuinely silly and the people warning against it were right.

But it took me until very recently to notice was that nobody, in all those arguments, had ever actually explained what the metric was *for*. What it was pointing at. Everyone, including me, was arguing about the number. Nobody was asking what the number was a proxy for.

It’s a proxy for **Conscious Coverage**. That’s the thing. Every line in the codebase is a decision. The question the metric is actually asking, underneath, is: *have you made a conscious decision about each one*. Not have you tested each one. Have you *decided* about each one. Tested, or consciously chosen not to test, with a reason, written down.

Concretely, it looks like this. You write a function with a branch that handles a malformed input. You run the coverage tool. It tells you the error branch isn’t covered. You now have three choices, and only three. 

1. You can write a test that exercises the malformed input and asserts the behaviour. 
2. You can mark the branch ignored with a comment that says, say, “unreachable because upstream validation guarantees this shape” — and now your justification is a reviewable artefact that someone can argue with in a pull request. 
3. Or you can decide the branch shouldn’t exist at all and delete it. What you cannot do is shrug and move on. The forgotten case is no longer a thing. Every line has had a decision made about it, and the decisions are legible.

```typescript
  ...
  static countryToRegion(countryCode: string): Region {
    /* v8 ignore start */ // Ignoring the switch to avoid repeating every single country code
    switch (countryCode) {
  ...
```

Once you see that, the version of the rule that the craft world rejected and the version the Economist team was running are obviously different things. The first one optimises for a number. The second one optimises for *the absence of accidents*. You can no longer fail to test something because you forgot. You can fail to test it because you decided not to, and you wrote down why, and someone can argue with you about it later in the review. The shape of the work is different.

And this is the bit I have to be honest about, because the post doesn’t work without it. Once the metric is framed as conscious coverage, the pragmatic position I’d absorbed at Cazoo stops being pragmatic. It’s just laziness with a vocabulary. “Write the tests that matter and let the rest go” sounds wise until you ask which lines, specifically, didn’t matter, and why, and the answer turns out to be that I didn’t want to write those tests and the tradition had given me a way to sound rigorous about not writing them. The metric wasn’t too expensive. The work it pointed to wasn’t too expensive. I just didn’t want to do it, and nobody was making me, and the craft vocabulary let me call that a considered trade-off.

I had to be in a place that just *did* it before I could see any of this. Sitting at Cazoo arguing about it from first principles, I would have lost the argument every time, because the version of the rule I was arguing against was the version everyone agrees is bad, and the version underneath it, the one about conscious, nobody had ever put into words for me. Nobody tells you the better version exists until you’re standing inside a codebase that runs on it.

## What changes when an agent is doing the writing

Fast forward. I’m now writing a lot of code with agents. Claude Code, Codex, OpenCode, the usual suspects. The thing I keep telling people who ask me about it is that agentic engineering requires *more* discipline than normal engineering, not less. The tools are faster, the output is bigger, and the gaps between what you asked for and what you got are easier to miss. So everything that used to depend on careful human attention now depends on something else holding the line. Which brings me back to the question: how do I know it’s done? And more importantly, how does an agent know?

Not “done” in the user-acceptance sense. Done in the much more boring sense of: has this thing actually exercised the code it claims to have written? Has it tested the behaviour I care about? Did it quietly skip a branch because the test was annoying to set up? Did it write something that’s technically passing but structurally untestable?

These are the questions the craftsmanship tradition spent twenty years building intuitions about, and the answer the tradition arrived at, pragmatically, contextually, with appropriate caveats, was mostly “you’ll know it when you see it, and pairing helps, and code review helps, and time helps.” Which is fine when humans are doing the work at human pace. It is not fine when an agent has just produced four hundred lines in ninety seconds and is asking what to do next.

The agent needs a guard rail. Something machine-checkable. Something it can run, get a number from, and decide for itself whether to keep going. Something another agent can validate. 

100% coverage, in the conscious sense, turns out to be exactly that. The agent finishes its loop, runs the coverage tool, sees 98%, and knows, without me telling it, that there are two percent of decisions it hasn’t made yet. Either write the test, or mark the lines as ignored with a justification. Both are fine. What’s not fine is leaving the gap.

And here is where the impact of the reframe gets outsized, because the agent doesn’t have my laziness. The agent doesn’t want to go home. The agent isn’t quietly negotiating with itself about which lines it can get away with skipping. The thing that was always standing between me and conscious coverage, which was me, just isn’t there. The metric stops being a rod I have to hold myself to and becomes a rod the agent holds itself to, cheerfully, at four in the morning, forever. The practice the craft tradition argued about most fiercely for human reasons becomes, for agents, the most natural thing in the world.

I’ve started using this as one of my standard acceptance criteria. “You are done when coverage reports 100%.” I can kick off a thirty-minute task and come back to something that, whatever else is true of it, will at least be testable, and will at least have had every line consciously decided about.

Coverage as the gate at the end works better when there’s a process upstream that’s likely to produce decent tests in the first place. If you set up the harness with CLAUDE.md files that push the agent toward red-green-refactor TDD, and you give it the kind of structured prompting (like obra/superpowers) that shapes how it actually approaches a task, you tilt the odds. There’s no guarantee it’ll write tests first. There’s a much better chance it will, and a much better chance the tests it writes are pulling the design rather than chasing it. That upstream tilt plus the downstream gate is a much sturdier system than either piece on its own.

There’s a sharpening of all this that matters, though, because coverage on its own can still produce tests that exercise code without actually testing anything. The companion practice, and I’d say it’s a necessary one rather than a complementary one, is writing tests outside-in, from behaviour rather than from structure. Test the unit of behaviour, not the unit of code. Don’t mock the internals; let the real thing run and assert against what the user of the code actually cares about. This was already the right answer when humans were writing the tests, because it produces tests that survive refactors and read like documentation. With agents it becomes critical, because a behaviour-shaped test is one the agent can write legibly from a user story, and one that you, as the reviewer, can read and check against intent without having to trace the implementation. Coverage tells you the agent made a decision about every line. Behavioural framing tells you the decisions were about the right things. You need both. Coverage without behavioural framing is theatre; behavioural framing without coverage leaves gaps you’ll find in production.

Now for the obvious objection. Agents are world-class metric gamers. They will absolutely write meaningless tests that exercise code without asserting anything useful. They will absolutely mark lines as ignored with justifications like “this branch is unreachable” when the branch is, in fact, reachable. If you treat 100% coverage as a number to satisfy, the agent will satisfy the number and you’ll be worse off than before, because now you have a green build hiding a problem instead of a red one announcing it.

The reason I think it works anyway is that it’s asking the right question of the metric. Coverage, in the conscious sense, is a completeness check. It tells you every line has had a decision made about it. It was never going to tell you the decisions were good ones. That’s a different question, and it wants a different answer. Behavioural tests, written outside-in from what the user of the code actually cares about, are the correctness check. Mutation testing, which flips operators and boundaries and asks whether any test notices, is the check on whether the assertions are doing real work. The gaming the agent does lives in the gap between those checks, and the mitigation isn’t to make coverage smarter. It’s to stop asking coverage to do correctness’s job. Use it for what it is: a completeness gate that makes the decisions visible. Use behavioural framing and mutation testing for the quality of the decisions. The ignored lines and their justifications are, at least, a reviewable artefact, sitting in one place where you can read them. The cheats are confined to a place you’re looking. None of that is automatic. It’s a discipline, and like every guard rail it collapses the moment you stop maintaining it. The question is whether the rail makes problems easier or harder to spot, and I think this one makes them easier.

## The truisms didn’t go away

The craft tradition produced a lot of practices, and a lot of arguments about practices, and a lot of nuance about when practices apply. Most of that nuance was about humans. About the cost of the practice to the person doing it, about whether the discipline was worth the friction, about whether the metric would be gamed. A lot of it, and I say this now having lived on both sides of the argument, was about whether the person doing the work would actually do it if you asked them to.

Agents don’t have that problem. The friction of writing the extra test isn’t a friction the agent feels. The discipline of marking ignored lines with reasons isn’t a discipline the agent has to be talked into. The kind of metric-gaming that comes from a tired human at five-to-six is replaced by a different kind of gaming, which is its own problem. So practices that were borderline-worth-it for humans become straightforwardly worth it for agents, and practices that were rejected as lunacy for humans turn out, on inspection, to have been rejected for reasons that said more about the humans than about the practice.

The craft was always about building software in a sustainable, predictable, maintainable way. That hasn’t changed. The agents don’t replace the craft. They inherit it. And some of the practices the tradition argued about most fiercely turn out, in this new context, to be exactly the load-bearing ones. Not because the old arguments were wrong about the metric, but because the old arguments were quietly also about us, and the us part has changed.

100% coverage wasn’t wrong. It was a proxy for something nobody I knew named. That allowed me to point at work I didn’t want to do, and dressed up in a vocabulary that let me agree with myself about not doing it. The agents don’t have the vocabulary and don’t need it. Which makes me wonder which other practices were rejected for reasons that were really about us, and what the calculation looks like now that we have a collaborator who just, straightforwardly, does the work. I’ve run that calculation for coverage. I’m increasingly sure it isn’t the only practice the answer flips for. I’d quite like to know which others.