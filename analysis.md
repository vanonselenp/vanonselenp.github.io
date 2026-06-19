# Blog Analysis — petervanonselen.com

_An objective, critical review of the live site and the full back catalogue. Conducted June 19, 2026._

## How this was done

I read every published page (Home, About, Start Here, Projects, Blog, Contact, Topics, and the eight tag pages) and all 40 posts from `2025-08-01` to `2026-06-17`, then cross-checked the live site, the rendered feed/sitemap/robots, and the Jekyll templates that produce them. Findings are grouped into **what's working**, **what can be improved**, **what isn't working**, a **gap analysis**, and a **prioritised action list**. There is a separate prior audit in the repo (`blog-interpretation-audit.md`); this is an independent read, though it reaches some of the same conclusions.

A one-line verdict up front: **the writing is the strongest asset here and it is genuinely good — but the site's packaging, navigation, identity signals, and conversion path are not yet doing that writing justice, and the back catalogue is uneven enough that a first-time visitor can easily land on a weak post and leave.**

---

## What's working

### 1. The 2026 essays are excellent and have a real point of view
The recent craft essays are the best thing on the site and would stand up on any engineering publication:

- **Money for Nothing** (2026-06-17) — feedback loops across decades, the trading engine, the GDPR basket table. Reframes "AI needs discipline" into something sharper: AI changes the *latency* of feedback, not the existence of the problem.
- **Encode It, Don't Remember It** (2026-06-07) — "put a small, dumb, deterministic thing in the path of a large, capable, non-deterministic one." A clean, quotable thesis with a concrete worked example.
- **Conscious Coverage** (2026-04-16) — genuinely original reframing of 100% coverage as "have you made a decision about each line," and why agents flip the cost/benefit.
- **The Canary in the Harness** (2026-04-12) and **The Council Will See You Now** (2026-04-03) — multi-harness working as regression detection. A non-obvious, well-argued idea.
- **The Best Part Has No AI in It** (2026-05-18) — "the most valuable AI products might not be very AI at all." Strong, contrarian, well-supported.

These pieces have a consistent intellectual throughline (discipline, feedback, harness-vs-model, the human as the judgement layer), original framings, and restraint. This is a defensible niche.

### 2. A coherent narrative arc
Read in order, the catalogue tells a real story: AI sceptic → Magic cube → board game → Godot game → spec-driven discipline → burnout → agentic katas → bringing it to the day job → print pipeline → production incidents → leaving one job for the next. The "learning in public" promise is actually kept. The honesty (failed refactors, burnout, "I should not have done this") is the differentiator and it's real.

### 3. Solid technical/SEO hygiene
- `jekyll-seo-tag`, JSON-LD `Person` schema, sitemap, full-content RSS (20 items, full HTML), `og:image` auto-extraction from the first in-content image, GA4.
- HTMLProofer runs in CI (`Links, Images, Scripts, OpenGraph`, `--enforce-https`) — link rot is actively guarded against.
- Redirects handled properly (`jekyll-redirect-from`) for renamed/unpublished posts; the unpublished `senior-staff-engineer` post 301s to home.
- Internal working docs (`specs/`, `tasks/`, `articles/`, `README.md`, the audit file) are excluded from the build — the sitemap is clean (56 URLs, no leaks). This was a real risk in the past and it's been closed.
- Accessibility basics present: skip link, `aria-label`s, alt text on most images.

### 4. Good entry-point design
**Start Here** is genuinely useful — it routes by reader intent ("I'm sceptical," "I lead engineers," "I want the gamedev story"). **Projects** is concrete and honest. The **Topics/tag** pages have hand-written intros rather than bare lists.

---

## What can be improved

### 1. Navigation of 40 posts is weak
The **Blog** page is a single flat reverse-chronological list of ~40 items. For a catalogue this size and this thematically split (gamedev devlog / AI craft essays / print pipeline / career-meta), a flat list is the wrong tool. A visitor who lands here has no way to see the shape of the work without scrolling 40 lines.

### 2. Post-to-post navigation jumps across unrelated threads
`post.html` only offers chronological **previous/next**. Because threads are interleaved by date, "next" from a gamedev devlog can be a production essay. Every post carries a `thread:` field in front-matter (`gamedev`, `craft`, `meta`) — **but nothing in the templates uses it.** There is dead metadata describing a feature that doesn't exist.

### 3. The site promises "thread groupings" it doesn't deliver
Three places tell the reader the blog is grouped by series:
- `start-here.md`: "the blog is chronological **with thread groupings**"
- `tags.md` / homepage: "**Threads on the blog page group by series**; tags group by topic"
- `projects.md`: "each with a thread of posts behind it"

The blog page has no thread groupings. It's a flat list. This is a broken promise the reader can immediately verify, and it undercuts trust. Either build the grouping (the `thread:` data is already there) or stop claiming it.

### 4. The early catalogue is much weaker than the recent work
The Aug–Dec 2025 gamedev devlogs are repetitive and tonally different from the essays that define the blog's value:
- The same beats recur (scope creep, "tangent king," "todo list," the distracted-boyfriend meme) across many posts.
- Heavy emoji, exclamation marks, and meme density (`:mindblown:`, "It was going to be over 9000!").
- This is fine as a devlog, but it clashes with the About page's stated audience ("engineers leading teams trying to separate real change from theatre"). A lead who arrives via a strong essay and clicks back into the archive may hit three "I got distracted again 😅" devlogs in a row.

This doesn't mean delete them — the arc matters — but they shouldn't be what a high-value visitor stumbles into first, and the homepage/Start Here should steer firmly toward the essays.

### 5. No subscription / audience-capture path
Every recent post ends with an invitation to engage ("Tell me what you build," "Let me know if you learn anything"). The only ways to follow are **RSS** and **LinkedIn**. There is no email capture, no newsletter. For a "learning in public" blog whose whole thesis is building an audience and a body of work, the absence of any subscribe mechanism is the single biggest missed conversion opportunity. Most readers don't use RSS.

### 6. Design is functional but dated and lacks dark mode
- Custom 687-line stylesheet, no dark mode (`prefers-color-scheme` unused) — notable for a developer audience that overwhelmingly browses dark.
- No reading-time estimate, no share affordance.
- Carousels are built with large blocks of inline styles and per-post `<script>` (the "An Army of One Prompt" NCO carousel duplicates logic that `model-carousel.html` already abstracts).

### 7. Thin / duplicate content
- **`2025-10-30-exert-of-what-i-learnt.md`** (260 words) is a near-verbatim excerpt of the 2025-10-20 post. Duplicate content with no canonical pointer — weak for SEO and weak for readers. (It also has the typo "exert" for "excerpt" baked into the slug.)
- **`2025-08-01-a-blog-of-dubious-intent.md`** (282 words) is thin and now duplicates the homepage intro.

### 8. Copy-editing and metadata errors
- Slug typos shipped to URLs: `exert-of-what-i-learnt`, `concious-coverage` ("conscious"), `chaos-cards-and-claude` (post title is actually "Cards, Chaos and...").
- In-body typos: "ithrough," "creatrure," "Wingum loop" vs "Wiggum loop" (inconsistent within the same arc), "betrayl."
- **Date issues:** `2025-09-15-boardgame-to-digital.md` has front-matter `date: 2025-09-07`, so it publishes on the **same date** as `building-ai-before-you-have-a-game` (filename says the 15th, the site says the 7th). `2026-03-05-the-feedback-that-doesnt-kill-you.md` carries front-matter date `2026-03-17` and a title ("...Doesn't Care About Your Title") that doesn't match its slug.
- Three posts have no `image:` front-matter; of those, `a-blog-of-dubious-intent` and `staff-engineer` and `exert...` have no in-content image either, so they get **no social card** when shared.

---

## What isn't working

### 1. Identity / name-collision is the biggest strategic problem
**"Peter van Onselen" is a well-known Australian political journalist and TV presenter.** Search results and LLM associations for the name are dominated by that person. For a blog whose growth depends on being found and correctly attributed ("who writes well about agentic coding practice?"), this is a serious headwind. The site does *some* disambiguation (JSON-LD: London, South African, Staff Engineer, `knowsAbout`), but:
- The `<title>` and tagline lead with "Staff Engineering & AI," not with anything that separates this Peter from the famous one.
- There is no explicit "not the journalist" signal, no distinctive personal-brand hook, and the name alone is a coin-flip for a new reader or an LLM.

This deserves a deliberate strategy (see actions).

### 2. Employer information is contradictory and stale
Three different signals, all live right now:
- **About page prose:** "a Staff Engineer, working on the **e-commerce funnel**" (this is the Economist-era description).
- **About page JSON-LD:** `worksFor` → **"Orbital.tech"**.
- **Recent posts (June 2026):** repeatedly state the author is **leaving The Economist** ("My final weeks at The Economist," "Soon I start somewhere new").

So the structured data says one employer, the prose implies another, and the latest narrative says he's departing. A recruiter, reader, or LLM gets three answers. The About page hasn't been updated to reflect the job change that the blog itself is announcing.

### 3. The About page contradicts its own structured data and the posts
Beyond the employer issue, the human-readable About reads as if nothing has changed since the Economist checkout-team role, while the most recent and most prominent posts ("The Machine Had Been Keeping a Diary," "Money for Nothing") are explicitly about closing out that job. The most-read part of the site is the least current.

### 4. No 404 page
There's no custom `404.html`; broken/old URLs fall back to GitHub Pages' generic 404 with no navigation back into the site. Given the history of renamed slugs, a branded 404 with links to Blog/Start Here would recover otherwise-lost visitors.

---

## Gap analysis (audience vs. delivery)

The About page names three target readers. Here's how well each is currently served:

| Target reader | Served? | Gap |
|---|---|---|
| **Sceptic who uses AI daily** | Well | The essays speak directly to them; Start Here routes them. Main risk is landing on a weak early devlog. |
| **Engineering leader separating signal from theatre** | Partially | The essays (Money for Nothing, Council, Canary, Best Part) are exactly for them — but the site's tone, emoji-heavy archive, and gamedev framing on the homepage/Projects can read as "hobbyist," undercutting authority. No exec-skimmable summaries. |
| **Wants to practise (katas)** | Partially | One post + a repo link. No standalone landing page for the katas, no "results of running the workshop" follow-up that was promised. |
| **Hobbyist gamedev / 3D-print** | Well | The devlogs and print-pipeline arc are thorough. But this audience barely overlaps with the AI-craft audience — see below. |

**The structural gap:** the blog is really *three blogs* (Godot gamedev devlog, AI-engineering essays, generative 3D-printing) sharing one feed. That's defensible as "learning in public," but it dilutes positioning. Someone subscribing for the production-engineering essays also gets miniature-printing support settings. There's no way to follow *one* thread. Tags help, but you can't subscribe to a tag, and the homepage doesn't let a visitor self-select a lane.

**Content gaps worth filling:**
- No "best of / start with these five" canonical list for the time-pressed (Start Here is intent-based, not a greatest-hits).
- The agentic-katas workshop follow-up ("I'll write about how it goes") was promised in March and hasn't landed — an open loop.
- No cross-linking between thematically related posts beyond a few manual "Related reading" footers (only the three newest posts have these).
- No canonical destination for the recurring `harness-bench` / dark-factory thread, which is clearly building toward something.

---

## Prioritised actions

### High impact, do first
1. **Fix the identity signals.** Decide on a disambiguation strategy from the famous journalist: lead the title/tagline and About with something unmistakably *this* Peter (e.g. "Staff engineer in London, learning AI-assisted development in public"), add an explicit line, and make sure the JSON-LD, About prose, and footer all agree.
2. **Reconcile the employer/About staleness.** Update About prose + JSON-LD to the actual current role (Orbital.tech?), and reflect the job change the blog is openly narrating. Pick one source of truth.
3. **Either build thread grouping or stop promising it.** The `thread:` data already exists on every post. Group the Blog page into collapsible series (Horizon's Edge, AI-assisted engineering, Print pipeline, Career & meta) and add same-thread prev/next on posts. This fixes navigation *and* the broken promise in one move.
4. **Add an email subscribe option** (Buttondown/Substack/ConvertKit embed). The whole site is built to grow an audience and currently has no front door for one.

### Medium impact
5. **Curate the front door.** Make the homepage and Start Here lead unambiguously with the strongest essays; consider a "Best of" list. Demote or clearly frame the early devlogs so a high-value visitor doesn't bounce off them.
6. **Prune/redirect thin & duplicate posts.** Redirect or rewrite `exert-of-what-i-learnt`; refresh or fold in `a-blog-of-dubious-intent`.
7. **Add dark mode** and a custom **404 page**.
8. **Copy-edit pass** for the shipped typos and fix the duplicate publish date (`boardgame-to-digital`) and the date/slug mismatches.

### Lower impact / polish
9. Reading-time estimates and a lightweight share affordance.
10. Social-card images for the three image-less posts.
11. Refactor the bespoke "Army of One Prompt" carousel to reuse `model-carousel.html`.
12. Close open loops: the katas workshop write-up, and a canonical page for the harness-bench/dark-factory thread.

---

## Open questions for the author

1. **Current employer:** Is Orbital.tech the new role, and should the About page now lead with it (or stay deliberately vague)? This blocks fixing the contradiction cleanly.
2. **Positioning:** Do you want this to be primarily the *AI-engineering essays* blog (with gamedev/print as colour), or a genuinely equal three-strand "learning in public" site? The answer changes navigation, homepage, and whether to split feeds.
3. **Audience goal:** Is the aim reach/readership (→ invest in subscribe + SEO + positioning), career/portfolio signalling (→ invest in About, disambiguation, case-study framing), or just a personal record (→ most of the above matters less)?
4. **The name problem:** Are you willing to lean into a more distinctive handle/brand to escape the journalist collision, or do you want to win the name on merit over time?
