---
layout: default
description: A staff engineer figuring out AI-assisted development in public — the tangents, the failures, and the learning.
---

<p class="site-tagline">A staff engineer figuring out AI-assisted development in public — the tangents, the failures, and the learning.</p>

This blog exists in the spirit of Austin Kleon's *Show Your Work*. You won't find polished tutorials here. Instead: scope creep documented in real-time, refactors that went sideways, a game that probably should have been paper-prototyped first, and the slow realisation that AI changes how you work but not how hard it is.

<div class="start-here" markdown="1">

## Start here

- **The origin story** — [A Blog of Dubious Intent](/2025/08/01/a-blog-of-dubious-intent/) — why this exists and what you'll find
- **The game** — [Finally... A Wild MVP Appears](/2025/12/04/finally-a-wild-mvp-appears/) — three months of building a tactical wargame with AI
- **The katas** — [How I Learnt to Stop Worrying and Love Agentic Katas](/2026/03/05/learn-to-love-agentic-coding/) — structured practice for AI-assisted development
- **The craft** — [The Smell of Panic When You Context Thrash](/2026/03/24/the-smell-of-panic-while-you-thrash/) — what goes wrong when you skip understanding

</div>

{% if site.posts.size > 0 %}
{% assign latest_post = site.posts.first %}
<div class="latest-post">
<h2>Latest</h2>
<h3><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h3>
<p class="post-meta">
    <time datetime="{{ latest_post.date | date_to_xmlschema }}">{{ latest_post.date | date: "%B %d, %Y" }}</time>
</p>

{{ latest_post.excerpt }}

<p><a href="{{ latest_post.url | relative_url }}">Read more &rarr;</a></p>
</div>
{% endif %}
