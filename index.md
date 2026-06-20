---
layout: default
description: A staff engineer figuring out AI-assisted development in public — the tangents, the failures, and the learning.
---

<p class="site-tagline">A staff engineer figuring out AI-assisted development in public ... the tangents, the failures, and the learning.</p>

This blog exists in the spirit of Austin Kleon's *Show Your Work*. You won't find polished tutorials here. Instead: scope creep documented in real-time, refactors that went sideways, a game that probably should have been paper-prototyped first, and the slow realisation that AI changes how you work but not how hard it is.

<div class="start-here" markdown="1">

## Start here

Want a primer of what I have learnt about agentic engineering? [Agentic Engineering &rarr;](/agentic-engineering/)

New here? [Find something that interests you... &rarr;](/start-here/)

</div>

{% if site.posts.size > 0 %}
{% assign latest_post = site.posts.first %}
<div class="latest-post">
<h2>Latest</h2>
<h3><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h3>
<p class="post-meta">
    <time datetime="{{ latest_post.date | date_to_xmlschema }}">{{ latest_post.date | date: "%B %d, %Y" }}</time>
</p>

{% assign latest_tagline = nil %}{% capture latest_tagline %}{% include tagline.html post=latest_post %}{% endcapture %}{% assign latest_tagline = latest_tagline | strip %}
{% if latest_tagline != "" %}<p class="post-tagline"><em>{{ latest_tagline }}</em></p>{% endif %}

<p>{% include first_paragraph.html post=latest_post %}</p>

<p><a href="{{ latest_post.url | relative_url }}">Read more &rarr;</a></p>
</div>

{% if site.posts.size > 1 %}
<section class="recently">
<h2>Recently</h2>
{% assign recent_posts = site.posts | slice: 1, 3 %}
{% for post in recent_posts %}
<div class="recently-post">
<h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
<p class="post-meta">
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
</p>

{% capture post_tagline %}{% include tagline.html post=post %}{% endcapture %}{% assign post_tagline = post_tagline | strip %}
{% if post_tagline != "" %}<p class="post-tagline"><em>{{ post_tagline }}</em></p>{% endif %}

<p>{% include first_paragraph.html post=post %}</p>

<p><a href="{{ post.url | relative_url }}">Read more &rarr;</a></p>
</div>
{% endfor %}
<p><a href="{{ '/blog/' | relative_url }}">See all posts &rarr;</a></p>
</section>
{% endif %}
{% endif %}
