# Spec: Homepage and craft fixes

**Blog:** petervanonselen.com (Horizons Edge)
**Scope:** Four discrete improvements identified from external review
**Non-goals:** Subscribe form, comments, share CTAs, thesis page, tag taxonomy redesign, dark-factory series. Voice and mission stay untouched.

---

## 1. Homepage teaser under Latest post

**Problem**

A cold visitor lands on the homepage and sees the latest post as a single line: title, date, tags. There is no excerpt, no sense of the writing. The strongest asset (the voice) does not get a chance to sell the click.

**Solution**

Auto-pull the first paragraph of the post body and render it as a teaser beneath the title block of the Latest entry on the homepage.

**Requirements**

- Source: the first prose paragraph of the post markdown, after any frontmatter and after the post's H1/title and any hero image.
- Skip: frontmatter, hero image markup, the H1, any subtitle or kicker line, any leading horizontal rule.
- Strip: inline markdown formatting (bold, italics, links rendered as plain text) so the teaser reads as clean prose. Preserve sentence punctuation exactly.
- Length: render the full first paragraph. No truncation, no ellipsis. If the first paragraph is unusually long (over ~80 words), that is a signal to edit the post, not the renderer.
- Only applies to the Latest block on the homepage. Does not affect /blog index, the "Start here" links, or the Recently strip (see section 2).
- The teaser is not a separate stored field. It is derived at build/render time from the post body.

**Acceptance**

- Loading the homepage shows the title, date, tags, and the first prose paragraph of the most recent post.
- The teaser matches the post body exactly (modulo formatting stripping).
- No teaser appears on any other surface.

---

## 2. "Recently" strip under Latest

**Problem**

A cold visitor on the homepage sees one Latest post next to four evergreen "Start here" links. They have no way to tell from the homepage whether the blog has 5 posts or 25. They have to navigate to /blog to find out. Most will not. The homepage understates the body of work.

**Solution**

Add a "Recently" strip directly beneath the Latest block. Three post titles with dates, in reverse chronological order, excluding the Latest post itself (so: posts 2, 3, and 4 by recency).

**Requirements**

- Heading: "Recently" (sentence case, same heading style as "Start here" and "Latest").
- Items: three posts, each rendered as title + date. No excerpts, no tags, no hero images. The Latest block does the heavy lifting; this strip is signal density.
- Order: reverse chronological, excluding the post shown in Latest.
- Each title links to the post.
- A small "See all posts →" link sits at the end of the strip, pointing to /blog.
- Visual weight: lighter than the Latest block. This is a glance-able list, not a second feature.
- Placement: between the Latest block and whatever currently sits beneath it (footer or other sections).

**Acceptance**

- A reader who never clicks past the homepage can see that four posts exist within a few weeks/months of each other (or however the cadence actually reads).
- The strip does not visually compete with the Latest block.
- The "See all" link reaches the existing /blog archive.

---

## 3. Craft fixes

**Problem**

Three small inconsistencies that undercut the otherwise careful prose. Individually trivial; collectively they suggest no final editing pass.

**Solution**

Three targeted edits.

**Requirements**

**3a. Panic post slug/title mismatch**
- Post: "The Smell of Panic When You Context Thrash"
- Current URL slug uses "while you thrash"; the title uses "when you"
- Decide canonical form (recommend matching the title: "when-you-context-thrash") and align the slug.
- If the slug changes, add a redirect from the old slug to the new one so existing links do not break.

**3b. Panic post subtitle typo**
- Current subtitle reads "High high hope for the code…"
- Almost certainly intended "High hopes" (likely a Pink Floyd reference). Confirm intent. If it was a typo, correct it. If it was deliberate, leave it and ignore this item.

**3c. Harness post table caption**
- Post: the harness benchmark post (with the "Median diff" column)
- Add a one-line caption directly under the table explaining the unit of measurement for "Median diff" (lines? files? characters?), so the reader does not have to infer it from prose two paragraphs later.

**Acceptance**

- Slug and title match. Old slug redirects.
- Subtitle is either corrected or confirmed deliberate.
- Harness table has a caption that explains the diff unit at the point the reader encounters it.

---

## 4. About page rewrite

**Problem**

The About page reads as a CV. The blog's mission is learning in public, practitioner-first, honest about tension. The About page should reflect that voice and purpose, not list job history.

**Solution**

Rewrite the About page so it answers, in order: what this blog is, who it is for, who is writing it, and what to expect. CV detail moves to a small "elsewhere" section at the bottom (LinkedIn link, GitHub link, current role mentioned in one line).

**Requirements**

- Voice: same register as the posts. Conversational, self-deprecating where natural, no em dashes, no bullets in the prose body.
- Length: roughly 250–450 words. Short enough to read in under two minutes.
- Structure (as prose, not headings):
  1. Opening: what the blog is and what it is trying to do. Learning-in-public framing. Honest about being practitioner-first, not thought leadership.
  2. Who it is for: sceptical engineers, active AI tool users, team leads. Phrased in the blog's voice, not as a marketing audience list.
  3. Who is writing it: staff engineer at The Economist, working on the e-commerce funnel. One or two lines on what that means for the perspective (production constraints, real systems, team context). No résumé prose.
  4. What to expect: cadence honesty (irregular, when there is something worth saying), the kind of content (essays not tutorials), and what the blog will not do (no promotional content, no clean resolutions, no tutorials).
- "Elsewhere" section at the bottom: LinkedIn, GitHub, contact email, RSS. Plain list is fine here; this is the one place bullets or a small link cluster reads correctly.
- Contact email: consider replacing the current iCloud address with a domain-matched address (hello@petervanonselen.com or similar). Out of scope to set up if it requires infrastructure work, but worth flagging in the same change.

**Acceptance**

- A first-time reader of the About page can answer: what is this blog, who is it for, who wrote it, and what should I expect, in under two minutes.
- The page reads in the same voice as a recent post.
- No em dashes. No bullets in the prose body. The "Elsewhere" cluster is the only structured element.

---

## Sequence

In order of effort and leverage:

1. Craft fixes (section 3) — under an hour, mostly mechanical.
2. Homepage teaser (section 1) — small template change.
3. Recently strip (section 2) — small template change, same pass as section 1.
4. About page rewrite (section 4) — the real writing work. Worth doing last so the homepage changes are live while the About page gets the attention it needs.

## Out of scope, explicitly

- Email subscribe form. Decided against on mission-fit grounds.
- Comments or webmentions. "Reply by email" remains the intended channel.
- Pinned thesis page. Conflicts with thesis-discovery-late preference.
- Tag taxonomy redesign. Tags remain as-is.
- Share CTAs, HN-shaped summaries, LinkedIn excerpts embedded in posts. LinkedIn remains a separate, deliberate channel.
- Projects page surfacing on homepage. Possible future work, not this spec.
