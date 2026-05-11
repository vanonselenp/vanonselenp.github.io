# PRD: Homepage and Craft Fixes

**Source spec:** `specs/001-update-to-site.md`
**Site:** petervanonselen.com (Jekyll, GitHub Pages)
**Branch suggestion:** `001-homepage-and-craft-fixes`

## 1. Introduction / Overview

The homepage currently shows the Latest post as a bare title-date-tags line with no excerpt, and gives no signal that more than one Latest + four "Start here" links exist. A cold visitor cannot taste the voice or sense the body of work. Separately, three small craft inconsistencies (a slug/title mismatch, a missing table caption) undercut otherwise careful prose, and the About page reads like a CV rather than the blog's voice.

This change makes four discrete improvements:

1. Render the first prose paragraph of the latest post as a teaser on the homepage.
2. Add a "Recently" strip beneath Latest listing posts 2–4 with a link to the full archive.
3. Three targeted craft fixes (slug rename + redirect; table caption on the harness post; the "High high hope" subtitle is confirmed deliberate and left untouched).
4. Rewrite the About page in the blog's voice, with a small "Elsewhere" cluster at the bottom.

Voice, mission, navigation, tag taxonomy, comments, subscribe form, share CTAs, and the "Start here" block stay untouched.

## 2. Goals

- A homepage visitor sees real prose from the latest post above the fold (or near it) before deciding whether to click through.
- A homepage visitor can tell at a glance that there are several recent posts, and reach the archive in one click.
- The "Smell of Panic" post has a canonical slug that matches its title, with the old URL preserved via redirect.
- The harness benchmark post's table is self-explanatory at the point the reader encounters it.
- The About page answers — in the blog's voice, under two minutes of reading — what the blog is, who it is for, who wrote it, and what to expect.

## 3. User Stories

### US-001: Render Latest post teaser on homepage
**Description:** As a cold visitor on the homepage, I want to read the first prose paragraph of the latest post so I can decide whether to click through based on the writing itself, not just the title.

**Acceptance Criteria:**
- [ ] The Latest block on `index.md` renders the first prose paragraph of the most recent post directly under the title/date.
- [ ] The teaser skips: frontmatter, any leading italic kicker/subtitle line (e.g. `_On discovering that..._`), leading horizontal rules (`---`), and any hero image (`![...](...)`) that appears before the first prose paragraph.
- [ ] Inline markdown formatting (bold, italics, links) is rendered as plain text in the teaser; sentence punctuation is preserved exactly.
- [ ] The full first paragraph is rendered with no truncation and no ellipsis.
- [ ] The teaser text matches the first prose paragraph of the underlying post body.
- [ ] No teaser is rendered on `/blog`, the "Start here" links, or the "Recently" strip (US-002).
- [ ] The teaser is derived at build time from the post body (not a new frontmatter field on every post).
- [ ] Verify in browser by loading `/` locally (`bundle exec jekyll serve`) and confirming the latest post's teaser matches the post body.

### US-002: Add "Recently" strip beneath Latest on the homepage
**Description:** As a visitor who never clicks past the homepage, I want to see that the blog has more than one post so I understand the body of work and can reach the archive easily.

**Acceptance Criteria:**
- [ ] A new "Recently" section appears on `index.md` directly beneath the Latest block (US-001), before any footer/other content.
- [ ] Heading text is `Recently`, rendered with the same heading style as `Start here` and `Latest` (i.e. `<h2>`).
- [ ] The strip lists exactly three posts: the 2nd, 3rd, and 4th most recent posts (i.e. excludes the post shown in Latest).
- [ ] Each item renders the post title (linked to the post) and its publication date. No excerpts, no tags, no hero images.
- [ ] Items are in reverse chronological order.
- [ ] A `See all posts →` link sits at the end of the strip, pointing to `/blog`.
- [ ] The strip has lighter visual weight than the Latest block (e.g. smaller titles, less vertical spacing) — it is a glance-able list, not a second feature.
- [ ] If fewer than four total posts exist, the strip renders whatever 2nd/3rd/4th posts do exist (graceful degradation), or hides if there are fewer than two posts.
- [ ] Verify in browser by loading `/` locally and confirming three posts are listed in correct order with the "See all" link reaching `/blog`.

### US-003: Rename panic post slug to match the title and add redirect
**Description:** As a reader, I want the URL of "The Smell of Panic When You Context Thrash" to match the title so the URL feels intentional and links remain coherent.

**Acceptance Criteria:**
- [ ] The post file `_posts/2026-03-24-the-smell-of-panic-while-you-thrash.md` is renamed to `_posts/2026-03-24-the-smell-of-panic-when-you-context-thrash.md`.
- [ ] The post's title in frontmatter remains `"The Smell of Panic When You Context Thrash"` (unchanged).
- [ ] The new canonical URL is `/2026/03/24/the-smell-of-panic-when-you-context-thrash/`.
- [ ] A redirect from the old URL (`/2026/03/24/the-smell-of-panic-while-you-thrash/`) to the new URL is in place. Implementation: use the `jekyll-redirect-from` plugin (already supported by GitHub Pages) by adding `redirect_from:` frontmatter to the renamed post, OR a stub file under the old path that issues a meta-refresh / 301-style redirect compatible with GitHub Pages.
- [ ] Internal links to the old slug anywhere in the repo are updated to point to the new slug. Specifically check: `index.md` (the "Start here" → "The craft" link currently points to the old slug), `blog.md`, any other posts that link to it, and `_config.yml` if it appears there.
- [ ] After a local build, visiting the old URL forwards to the new URL; visiting the new URL renders the post.
- [ ] The subtitle "High high hope for the code…" is confirmed deliberate and is left unchanged (no edit).

### US-004: Add an in-place caption to the harness post's "Median diff" table
**Description:** As a reader of the harness benchmark post, I want to know the unit of measurement for the "Median diff" column at the moment I see the table, so I do not have to infer it from prose two paragraphs later.

**Acceptance Criteria:**
- [ ] Identify the harness benchmark post in `_posts/` (the one containing a table with a `Median diff` column). Record the file path in the PR/commit so it is auditable.
- [ ] Determine the unit of measurement for `Median diff` by reading the surrounding prose of the post (the unit is described later in the post). Document the unit in the PR description.
- [ ] Add a one-line caption directly beneath the table that states the unit, in the post's voice. Example shape: `*Median diff measured in lines of code per change.*` (Use the actual unit; this is illustrative.)
- [ ] The caption uses the same markdown emphasis style already used in the post for similar inline notes (typically `_italic_` or `*italic*`).
- [ ] No other content of the post is changed.

### US-005: Rewrite the About page in the blog's voice with an "Elsewhere" cluster
**Description:** As a first-time reader of the About page, I want to understand what the blog is, who it is for, who wrote it, and what to expect — in the same voice as a recent post and in under two minutes — so the About page reflects the blog's mission rather than reading like a CV.

**Acceptance Criteria:**
- [ ] `about.md` is rewritten as prose (no headings inside the body) following the four-beat structure in the spec, in this order:
    1. What the blog is and what it is trying to do (learning-in-public framing; practitioner-first; not thought leadership).
    2. Who it is for (sceptical engineers, active AI tool users, team leads — phrased in the blog's voice, not as a marketing audience list).
    3. Who is writing it (staff engineer at The Economist + one or two lines on what that perspective brings — see Open Question OQ-1 about the specific team description).
    4. What to expect (cadence honesty: irregular, when there is something worth saying; essays not tutorials; what the blog will not do: no promotional content, no clean resolutions, no tutorials).
- [ ] Total prose body length is 250–450 words.
- [ ] No em dashes (`—`) anywhere in the prose body. (Hyphens and en dashes are fine; em dashes specifically are out.)
- [ ] No bullets in the prose body. The "Elsewhere" cluster is the only structured element on the page.
- [ ] Voice matches a recent post (conversational, self-deprecating where natural, no hype, no marketing register).
- [ ] An "Elsewhere" section sits at the bottom of the page, after the prose. It lists, as a small cluster:
    - LinkedIn (existing link, preserved from current `about.md`)
    - GitHub (existing link, preserved from current `about.md`)
    - Contact email (see OQ-2 about domain-matched address)
    - RSS feed (`/feed.xml`)
    - Optionally: one line stating current role ("Staff Engineer at The Economist") as flat prose, not as a CV.
- [ ] The existing `schema.org` JSON-LD `<script>` block is preserved (or updated only if the email/role decisions change it).
- [ ] The draft prose is provided in the PR for review before being merged; revisions from the author are expected before sign-off.
- [ ] Verify in browser by loading `/about/` locally and confirming the page renders, the prose is in voice, and the "Elsewhere" cluster reaches the correct external links.

## 4. Functional Requirements

- **FR-1:** The homepage template (`index.md` and/or a partial it uses) must derive the first prose paragraph of the latest post at build time, stripping leading frontmatter artefacts, italic kicker subtitle, leading `---` horizontal rule, and leading hero image markdown image (`![alt](url)`).
- **FR-2:** The teaser rendering must strip inline markdown formatting (bold, italics, links) to plain text, while preserving sentence punctuation.
- **FR-3:** The homepage must render a "Recently" section beneath Latest containing the 2nd, 3rd, and 4th most recent posts (title + date + post link).
- **FR-4:** The "Recently" section must include a `See all posts →` link to `/blog`.
- **FR-5:** The post file for "The Smell of Panic When You Context Thrash" must be renamed so its generated URL is `/2026/03/24/the-smell-of-panic-when-you-context-thrash/`.
- **FR-6:** A redirect from `/2026/03/24/the-smell-of-panic-while-you-thrash/` to the new URL must be in place at build time.
- **FR-7:** All internal references in the repo to the old panic-post slug must be updated to the new slug.
- **FR-8:** The harness benchmark post must have a one-line caption immediately beneath its `Median diff` table, stating the unit of measurement.
- **FR-9:** `about.md` must be rewritten to the structure, voice, and length defined in US-005.
- **FR-10:** `about.md` must contain an "Elsewhere" cluster at the bottom listing LinkedIn, GitHub, contact email, and RSS.
- **FR-11:** No em dashes (`—`) and no bullets in the About page prose body. Bullets are only permitted in the "Elsewhere" cluster.
- **FR-12:** All changes must build cleanly under the existing Jekyll + GitHub Pages configuration (no new gem dependencies beyond what GitHub Pages already supports; `jekyll-redirect-from` is supported).

## 5. Non-Goals (Out of Scope)

- Email subscribe form. (Decided against on mission-fit grounds.)
- Comments or webmentions. "Reply by email" remains the channel.
- Pinned thesis page. Conflicts with thesis-discovery-late preference.
- Tag taxonomy redesign. Tags remain as-is.
- Share CTAs, HN-shaped summaries, LinkedIn excerpts embedded in posts.
- Projects page surfacing on the homepage.
- The "High high hope for the code…" subtitle — confirmed deliberate, left untouched.
- Setting up the domain-matched contact email address (e.g. `hello@petervanonselen.com`). Flagged as a follow-up in OQ-2.
- Truncation / ellipsis logic on the teaser. If a first paragraph is unusually long, the fix is to edit the post, not the renderer.
- Adding teasers anywhere other than the Latest block on the homepage (`/blog`, "Recently" strip, "Start here" links remain teaser-free).

## 6. Design Considerations

- **Latest block:** keep existing visual hierarchy. Teaser is body text; the title and date stay as the headline elements.
- **Recently strip:** visually lighter than Latest. Suggested treatment: smaller heading weight, single-line list, no card framing. The strip should read as "and there's more over there," not as a second feature block.
- **Existing CSS classes to reuse:** `latest-post`, `start-here`, `post-meta`, `site-tagline` (see `index.md`). A new class such as `recently` will likely be needed; mirror the structure and spacing of `start-here` but with reduced weight.
- **About page:** prose-first layout under the existing `page` layout. The "Elsewhere" cluster can reuse footer-style link grouping or a simple `<ul>` with custom class.
- **Mobile:** all changes must read cleanly at narrow widths. The "Recently" strip should not introduce horizontal scrolling.

## 7. Technical Considerations

- **Stack:** Jekyll site built by GitHub Pages. Layouts in `_layouts/`, posts in `_posts/`, homepage in `index.md`.
- **Latest excerpt today:** `index.md` already renders `{{ latest_post.excerpt }}`. Jekyll's default `excerpt` is everything up to the first `excerpt_separator` (default: blank line / `\n\n`). For posts that lead with an italic kicker line, the rendered excerpt is the kicker — not the first prose paragraph. The fix needs custom Liquid logic to skip kicker, `---`, and hero image lines and then take the first prose paragraph. Consider implementing as an include (`_includes/first_paragraph.html`) so the logic is testable and reusable.
- **Redirects:** GitHub Pages supports `jekyll-redirect-from`. Add to `_config.yml` plugins list if not present, then add `redirect_from: [/2026/03/24/the-smell-of-panic-while-you-thrash/]` to the renamed post's frontmatter.
- **Renaming a post file** changes the generated URL (`permalink` is derived from filename + date). Verify the new URL renders before merging.
- **JSON-LD schema** in `about.md` references the email and role. If the role wording or email changes (OQ-1, OQ-2), update the schema accordingly to avoid silent drift.
- **No new dependencies** should be added beyond what GitHub Pages whitelists.
- **Local verification:** `bundle exec jekyll serve` should be used to verify all changes before raising the PR.

## 8. Success Metrics

- A cold visitor on the homepage can read at least one full paragraph of recent prose without clicking.
- A cold visitor on the homepage can see at least four post titles (1 in Latest, 3 in Recently) and reach the archive in one click.
- Visiting the old panic-post URL forwards to the new one and does not 404.
- A first-time reader of `/about/` can answer in their own words: what is this blog, who is it for, who wrote it, what should I expect — in under two minutes.
- The About page contains zero em dashes and zero bullets in its prose body.

## 9. Open Questions

- **OQ-1 (About page, role wording):** The source spec says "staff engineer at The Economist, working on the e-commerce funnel." The current `about.md` says "backend systems, cloud infrastructure, and developer experience." These are different. Confirm which is current and accurate before the About page rewrite is drafted. The PRD assumes the spec is authoritative but will defer to the author's correction.
- **OQ-2 (Contact email):** The current `about.md` JSON-LD lists `augury_upsurge.17@icloud.com`. The spec suggests considering a domain-matched address (`hello@petervanonselen.com` or similar) but flags setup as potentially out of scope. Decision needed:
    - Keep iCloud address visible in "Elsewhere"; OR
    - Use a placeholder domain-matched address and flag DNS/forwarding setup as a follow-up task; OR
    - Leave email out of "Elsewhere" entirely and rely on the existing `contact.md` page.
- **OQ-3 (Harness post identity):** US-004 requires identifying which post is "the harness benchmark post" with the `Median diff` column. The implementer should grep `_posts/` for `Median diff` and confirm the file before editing. If more than one post matches, raise the ambiguity in the PR before editing.
- **OQ-4 (Recently strip — fewer than 4 posts edge case):** Should not be hit in practice (the blog has 30+ posts), but worth confirming: if posts < 2, hide the strip entirely; if posts 2–3, show whatever 2nd/3rd posts exist. Confirm this graceful-degradation behaviour is acceptable.
- **OQ-5 (Teaser stripping — edge cases):** What should happen if a post's first prose paragraph contains a footnote reference (`[^1]`) or an inline image inside the paragraph? The spec is silent. Reasonable default: footnote references render as plain text marker stripped; inline images mid-paragraph are rare in this blog's posts and can be handled if/when one appears.

## 10. Implementation Sequence (from the spec)

1. Craft fixes — US-003, US-004. Mechanical, under an hour.
2. Homepage teaser — US-001. Small template change.
3. Recently strip — US-002. Same pass as US-001.
4. About page rewrite — US-005. The real writing work; do last so homepage changes ship while the About page gets the attention it needs.
