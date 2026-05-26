# Blog Interpretation-Economy Audit — petervanonselen.com

**Date:** 2026-05-18
**Scope:** How readily AI agents (ChatGPT search, Claude, Perplexity, Google AI Overviews, etc.) can crawl, understand, and accurately attribute the content on petervanonselen.com.
**Method:** Read-only inspection of the Jekyll source (`_config.yml`, layouts, `_includes`, `_posts/*.md`, `about.md`, `blog.md`, `index.md`, `projects.md`, `contact.md`) and the built site under `_site/` (representative posts, `sitemap.xml`, `robots.txt`, `feed.xml`, About, Home). One spot check against the live `robots.txt` over the network.

The site is in genuinely good shape for crawlers — Jekyll renders static HTML, `jekyll-seo-tag` is wired up, the About page already has a `Person` JSON-LD block, the Atom feed is full-content. There are no BLOCKING failures. The improvements are about *disambiguation* (there's another well-known Peter van Onselen) and *summary surface* (descriptions, OG images, thesis statements) — the two things an AI agent leans on hardest when asked "who writes well about X?".

---

## Findings by Section

### 1. Structured Data

| # | Finding | Severity |
|---|---------|----------|
| 1.1 | `jekyll-seo-tag` emits `BlogPosting` JSON-LD on every post with `headline`, `datePublished`, `dateModified`, `description`, `url`, `mainEntityOfPage`. Good baseline. | — |
| 1.2 | `BlogPosting.author` on posts is `{ "@type": "Person", "name": "Peter van Onselen" }` only — no `@id`, no `sameAs`, no `url`. Agents cannot reliably link the post's author to the canonical `Person` block on `/about/`. Critical because the name collides with a high-profile Australian journalist. | **HIGH** |
| 1.3 | About page (`about.md` lines 25–63) has a rich `Person` JSON-LD: `jobTitle`, `worksFor`, `sameAs` (GitHub + LinkedIn), `address`, `nationality`, `knowsAbout`, `description`. Excellent — but it is *not referenced* from `BlogPosting.author` on posts, so the linkage is implicit at best. | **HIGH** (fix in tandem with 1.2) |
| 1.4 | No `image` field on `BlogPosting`. Google AI Overviews and other agents prefer to surface a thumbnail; without one, posts are less likely to be cited with a card. | MEDIUM |
| 1.5 | No `publisher` on `BlogPosting`. Google's Rich Results validator warns on this. Should be an `Organization` (or self-publisher `Person`). | MEDIUM |
| 1.6 | No `keywords` / `articleSection` on `BlogPosting`, even though every post has `categories` in frontmatter. Free signal being thrown away. | MEDIUM |
| 1.7 | Homepage emits `WebSite` JSON-LD with `sameAs` and `author`. Good. No `SearchAction` (site search) — minor. | LOW |
| 1.8 | No site-wide `Organization` / `Brand` schema. For a personal blog this is acceptable — the `Person` is the entity. | LOW |
| 1.9 | Two `<meta name="description">` tags appear on every rendered page — one from `_layouts/default.html` line 7, one from `{% seo %}` inside `jekyll-seo-tag`. The two often disagree (post-specific vs site-wide). Crawlers will pick one and you don't control which. | **HIGH** |

### 2. Crawlability

| # | Finding | Severity |
|---|---------|----------|
| 2.1 | `sitemap.xml` exists (auto via `jekyll-sitemap`), 44 URLs, last-mod times present. | — |
| 2.2 | Sitemap leaks internal planning docs: `/specs/001-update-to-site.html`, `/tasks/prd-homepage-and-craft-fixes.html`, and `/articles/horizons-edge/5-command-token-bag-system.html`. These are not in the published blog index, but agents will crawl, ingest, and potentially cite them. They read as raw working notes. | **HIGH** |
| 2.3 | `robots.txt` (`_site/robots.txt`, served live) contains only `Sitemap: …` — no `User-agent` directives at all. By convention this means *all* user-agents are allowed including `GPTBot`, `ClaudeBot`, `PerplexityBot`, `Google-Extended`, `CCBot`, etc. This is the right outcome for an author who *wants* to be retrievable; making it explicit removes ambiguity. | LOW (policy call) |
| 2.4 | No `noindex` tags anywhere. No accidental crawl blocks. | — |
| 2.5 | URLs are clean, dated, semantic (`/YYYY/MM/DD/slug/`). Stable. | — |
| 2.6 | No `/llms.txt` (emerging Anthropic-coined convention) summarising the site for LLM context. | LOW |

### 3. Semantic HTML

| # | Finding | Severity |
|---|---------|----------|
| 3.1 | Each post's `<h1>` is the actual post title (`_layouts/post.html` line 7), not the site name. | — |
| 3.2 | `<article>`, `<main id="main-content">`, `<header>`, `<footer>`, `<nav aria-label>` all present and well used. | — |
| 3.3 | Dates use `<time datetime="…">` with ISO-8601 (`_layouts/post.html` line 9, `index.md` line 27, `blog.md` indirectly). | — |
| 3.4 | Author is plain `<p>` text in the post footer. No `rel="author"`, no `<address>`, no link to a `Person` URI. Combined with finding 1.2 this is why disambiguation is weak. | MEDIUM |
| 3.5 | Categories are `<span class="category">…` (visual styling only). They are not clickable, not linked to taxonomy pages, and not exposed in structured data. | MEDIUM |
| 3.6 | Heading hierarchy in posts is healthy (single `<h1>`, sub-sections use `<h2>`/`<h3>`). | — |

### 4. Metadata

| # | Finding | Severity |
|---|---------|----------|
| 4.1 | **No post has a `description:` in its frontmatter.** Of 35 posts in `_posts/`, 0 have `description:`, 1 has `excerpt:`. Result: `jekyll-seo-tag` derives the description from the first paragraph, which on this blog is almost always a *hook* / scene-setter, not a thesis. Example: the post "The Best Part Has No AI in It" gets meta description "On building the plumbing between the prompts." — fine because that post's italic opener happens to be a tagline. Most posts open with anecdote; the agent gets the anecdote instead of the argument. | **HIGH** |
| 4.2 | Page-level metadata on `about.md`, `projects.md`, `contact.md`, `blog.md` is good — explicit `description` strings. | — |
| 4.3 | Canonical URL is set per page by `jekyll-seo-tag`. | — |
| 4.4 | Open Graph: `og:title`, `og:description`, `og:url`, `og:site_name`, `og:type`, `og:locale`, `og:article:published_time` all present. **`og:image` is missing site-wide.** No frontmatter `image:` on any of the 35 posts. Result: Twitter card is `summary` (small), not `summary_large_image`; social previews and AI-citation cards have no visual. | **HIGH** |
| 4.5 | Titles are distinctive and information-dense in some places ("The Smell of Panic When You Context Thrash", "14 PRs, 6 Repos, 1 Button"), but several are *only* clever ("Your Scientists Were So Preoccupied", "Show Your Work", "This Is the Way: Delete the Code"). Without a strong description, an agent answering "find me writing about AI-assisted refactoring" has no signal that "Your Scientists Were So Preoccupied" is about SSHing into Claude Code from a phone. | MEDIUM |
| 4.6 | `<meta name="generator">` is `Jekyll v3.10.0` — harmless. | — |

### 5. Content Legibility for Agents

| # | Finding | Severity |
|---|---------|----------|
| 5.1 | Posts almost never lead with a thesis sentence. They open with anecdote ("A friend of mine just got a 3D printer…"), italic tagline, or scene-setting. Excellent prose; bad summarisation surface. Combined with finding 4.1 this is the single biggest interpretation-economy weakness. | **HIGH** |
| 5.2 | When concrete evidence appears it is good — specific numbers ("fifty models", "three evenings", "forty-one models", "Cazoo", "The Economist", "e-commerce funnel"). Agents *can* cite these once they find them. | — |
| 5.3 | About page (`about.md` lines 8–16) is strong: clearly states who Peter is, where, what he does, who the writing is for. An agent asked "who is this?" gets a useful two-sentence summary. | — |
| 5.4 | `blog.md` thread-groups posts into "Horizon's Edge", "AI-Assisted Engineering", "Career & Meta" with descriptive sub-headings. Good for an agent trying to map areas of expertise — *if* the agent reads it. But these groupings exist only as `<details>` summaries on a single page; they are not first-class taxonomy URLs. | MEDIUM |
| 5.5 | No `/topics/` or `/categories/{slug}/` index pages despite the `categories:` frontmatter on every post. Agent has no canonical URL for "Peter's writing about agentic katas" to cite. | MEDIUM |
| 5.6 | No "now"/"uses"/CV page. CV PDF exists at `/assets/resume.pdf` and is in the sitemap — agents will find it, but it's not linked from About. | LOW |

### 6. Entity Disambiguation

| # | Finding | Severity |
|---|---------|----------|
| 6.1 | "Peter van Onselen" is a well-known Australian political journalist. An agent asked "who writes well about agentic coding practice" and finding this site needs an unambiguous signal that *this* Peter is the London-based Staff Engineer at The Economist, not the Australian academic. The About page's `Person` JSON-LD does this clearly (London, South African, Staff Engineer, knowsAbout list, GitHub + LinkedIn). | — |
| 6.2 | Posts do NOT link their author to the About `Person` block. `BlogPosting.author` is name-only. An agent reading a single post in isolation (e.g. via an RSS scrape or a deep link) has no schema-level signal to disambiguate. | **HIGH** |
| 6.3 | `sameAs` is present on About-page `Person` and on homepage `WebSite.sameAs`, listing GitHub and LinkedIn. Not present on post-level `BlogPosting.author`. | (fixed by 6.2) |
| 6.4 | Footer prose on every post says "I'm Peter, a Staff Engineer at The Economist" — useful disambiguation, but prose only. | — |

### 7. RSS / Feeds

| # | Finding | Severity |
|---|---------|----------|
| 7.1 | Atom feed at `/feed.xml` via `jekyll-feed`, linked in `<head>` via `{% feed_meta %}` (`_layouts/default.html` line 27). | — |
| 7.2 | Feed includes full HTML content of posts (verified on latest post). | — |
| 7.3 | `feed.posts_limit: 20` in `_config.yml`. With 35 posts, the feed already omits the oldest ~15. Most aggregators only need recent items, but AI crawlers that snapshot the feed will miss the "origin story" posts. | LOW |

### 8. Performance / Rendering

| # | Finding | Severity |
|---|---------|----------|
| 8.1 | Static HTML, server-rendered at build time. No JS dependency for content visibility. Ideal for AI crawlers. | — |
| 8.2 | Image `alt` text is highly variable. Many decorative/jokey alts: `alt="hero image"`, `alt="cropper"`, `alt="current"`, `alt="banner"`, `alt="this is fine, right?"`, `alt="mage!"`. Few alt strings describe what the image actually shows. Acceptable for accessibility (decorative is allowed) but misses an information surface for agents doing image-text alignment. | MEDIUM |
| 8.3 | No `loading="lazy"` on images — fine for crawlers (they ignore it), worth knowing but not in scope. | — |
| 8.4 | Google Analytics tag is third-party JS but does not block content rendering. | — |

---

## Summary of Severities

- **BLOCKING:** none.
- **HIGH:** 7 findings — 1.2/1.3 (post author not linked to canonical Person), 1.9 (duplicate `<meta name="description">`), 2.2 (internal specs/tasks in sitemap), 4.1 (no post descriptions, thesis is auto-derived from first paragraph), 4.4 (no `og:image` site-wide), 5.1 (no explicit thesis statements), 6.2 (entity disambiguation weak at post level).
- **MEDIUM:** 1.4, 1.5, 1.6, 3.4, 3.5, 4.5, 5.4, 5.5, 8.2.
- **LOW:** 1.7, 1.8, 2.3, 2.6, 5.6, 7.3.

---

## Prioritised Task List (concrete fixes)

The list below is ordered by impact on AI agent comprehension per unit of effort. File paths are repo-relative.

### P0 — biggest payoff, smallest change

**T1. Remove the duplicate `<meta name="description">` tag.** *(Severity 1.9)*
- File: `_layouts/default.html` lines 6–7.
- Change: delete the hand-rolled `<title>` and `<meta name="description">` lines; let `{% seo %}` own both. (`jekyll-seo-tag` already emits a correct title and description; the duplicate is fighting it.)
- Suggested diff: remove lines 6 and 7 entirely.

**T2. Add `description:` to every post's frontmatter.** *(Severity 4.1, 5.1)*
- Files: all 35 files in `_posts/*.md`.
- Constraint: 140–160 chars, one sentence, states the *argument or claim*, not the opening hook. Example for `2026-05-18-best-part-has-no-ai-in-it.md`:
  `description: "The most valuable AI products may have very little AI in them. They automate the cruft around the model so humans can spend time on the decisions."`
- This is the single highest-leverage change. Treat it as one batch task.

**T3. Add `image:` to every post's frontmatter and let `jekyll-seo-tag` emit `og:image`.** *(Severity 4.4, 1.4)*
- Files: all 35 files in `_posts/*.md`.
- Most posts already include a hero `![…](/assets/…)` on line 1–3 of the body. Reuse it: `image: /assets/best-part/hero.png`.
- After fix, also switch the Twitter card to `summary_large_image` (configured via `twitter.card` in `_config.yml`).

**T4. Link `BlogPosting.author` to the canonical `Person`.** *(Severity 1.2, 1.3, 6.2)*
- This requires overriding `jekyll-seo-tag`'s author emission. Two options:
  - (a) Set `author:` in `_config.yml` to a mapping that includes `url`/`sameAs` (the `jekyll-seo-tag` README documents this; it will propagate to `BlogPosting.author`).
  - (b) Inject a small extra JSON-LD block in `_layouts/post.html` that defines `"@id": "https://www.petervanonselen.com/#peter"` for the `Person` and references it from the post.
- Recommended: option (a). In `_config.yml`, expand the existing `author:` mapping with `url`, `sameAs` (github + linkedin), and `image`. `jekyll-seo-tag` will then output the full `Person` inside the post JSON-LD, including `sameAs`, which is what an agent needs to disambiguate from the journalist.

**T5. Stop publishing `_specs/` and `_tasks/` as crawlable pages.** *(Severity 2.2)*
- Files involved: `specs/001-update-to-site.md`, `tasks/prd-homepage-and-craft-fixes.md`, and the entire `articles/` tree if it is not intended for readers.
- Options (pick one per directory):
  - Move them under a directory starting with `_` (Jekyll convention: `_specs/`, `_tasks/`) and don't create a collection for them, or
  - Add them to `exclude:` in `_config.yml`, or
  - Add `sitemap: false` to each file's frontmatter (this only removes from sitemap; the file is still served if URL is known).
- Recommended: `exclude:` in `_config.yml` for `specs/` and `tasks/`. Decide separately whether `articles/horizons-edge/` is published-for-readers or internal.

### P1 — meaningful improvements, more files touched

**T6. Add a "TL;DR" or thesis paragraph to each post.** *(Severity 5.1)*
- For each post in `_posts/*.md`, prepend a short bolded sentence after the title/byline that states the argument in agent-citation form. Example:
  > **TL;DR — the best AI tooling automates the cruft around the model, not the model itself.**
- Lower priority than T2 because the meta `description` covers most of this, but humans reading via search-preview cards also benefit.

**T7. Add an explicit `robots.txt` listing AI bots.** *(Severity 2.3)*
- File: create `robots.txt` at repo root (it will pass through `jekyll-sitemap`'s default and overwrite the auto-generated one).
- Content (assuming "allow all" is the policy):
  ```
  User-agent: *
  Allow: /

  User-agent: GPTBot
  Allow: /

  User-agent: ClaudeBot
  Allow: /

  User-agent: PerplexityBot
  Allow: /

  User-agent: Google-Extended
  Allow: /

  User-agent: CCBot
  Allow: /

  Sitemap: https://www.petervanonselen.com/sitemap.xml
  ```
- This is a policy decision. Document the intent ("This blog is intended to be cited by AI assistants; I am opting in explicitly").

**T8. Add `keywords` and `publisher` to BlogPosting JSON-LD.** *(Severity 1.5, 1.6)*
- `jekyll-seo-tag` includes `keywords` from frontmatter automatically. Add `tags:` or set `keywords:` per-post (or reuse `categories:`).
- For `publisher`, either:
  - Set `author:` mapping in `_config.yml` to include `logo` (this becomes the publisher via plugin convention), or
  - Override `_includes/jekyll-seo-tag/json_ld.html` in your includes.

**T9. Surface categories as first-class taxonomy pages.** *(Severity 3.5, 5.4, 5.5)*
- Generate `/categories/{slug}/` index pages, each listing posts in that category with a one-line `description`. With GitHub Pages plugin allowlist, the cleanest path is the `jekyll-archives` plugin (not on the GitHub Pages allowlist — would need GH Actions build, which this repo already uses).
- Cheap alternative: manually create a small set of `/topics/{slug}.md` pages for the highest-value taxonomies ("AI-assisted engineering", "Agentic katas", "Game development"). Link them from `about.md`. Less complete, but doable without new plugins.

**T10. Improve image alt text.** *(Severity 8.2)*
- Audit `_posts/*.md` for `![cropper]`, `![hero image]`, `![banner]`, `![current]`, `![mage!]`, etc.
- Replace with descriptive text. For purely decorative images, keep alt short but on-topic. For images carrying information (UI screenshots, diagrams), describe what is shown.

### P2 — polish

**T11. Add `/llms.txt`.** *(Severity 2.6)*
- File: create `llms.txt` at repo root.
- Content: short author/site description + a curated list of canonical post URLs grouped by theme (mirrors the `blog.md` thread structure but in plain text). Acts as a hand-built summary for LLMs.

**T12. Raise `feed.posts_limit` or remove the cap.** *(Severity 7.3)*
- File: `_config.yml` line 22. Change `posts_limit: 20` to `posts_limit: 50` (or remove).

**T13. Add a `<address rel="author">` (or `<p rel="author">`) wrapping the byline.** *(Severity 3.4)*
- File: `_layouts/post.html` lines 23–27. Wrap the author footer in `<address rel="author" itemprop="author">` to give it semantic weight beyond JSON-LD.

**T14. Add a SearchAction to WebSite JSON-LD.** *(Severity 1.7)*
- Only useful if site search exists. There is no site search now; defer until there is one.

**T15. Re-link CV from About.** *(Severity 5.6)*
- `assets/resume.pdf` is in the sitemap but not linked from `about.md`. Add a line to the "Elsewhere" list: `- [CV / Resume](/assets/resume.pdf)`.

---

## Notes / Out of Scope

- All findings are based on the source repo at HEAD and a single live network check on `robots.txt`. I have not run the live rendered HTML through a Schema.org validator or a Google Rich Results test; doing so is recommended after T1–T5 land.
- The blog's prose style — anecdote-led, italic taglines, no TL;DR — is part of its voice. T2 (frontmatter `description`) is the right fix: it gives agents a clean handle without changing the writing. T6 (in-post TL;DR) is offered as optional.
- If the policy decision in T7 goes the other way (opt *out* of AI crawlers), the change is the same file but with `Disallow: /` blocks per bot. The current live state is "allowed by default".
