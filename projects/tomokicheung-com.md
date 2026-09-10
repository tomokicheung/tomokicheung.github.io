---
layout: project
type: project
image: img/tomokicheung/tomokicheung-square.png
title: "tomokicheung.com"
date: 2026-09-09
published: true
labels:
  - Astro
  - Cloudflare Workers
  - TypeScript
  - Web Security
summary: "My personal site, rebuilt from a single 5.5MB HTML file into a static Astro build with the reasoning behind every decision written down in the public repository."
---

tomokicheung.com is my personal site. I own the domain and I wanted one place under my own name holding my client work, my writing, and a record of what I have been doing. The starting material was a single HTML file I had written earlier in the year. It was 5,529,152 bytes, of which about 73,000 was actual code. The rest was sixteen images encoded as base64 text and pasted inline, which inflated 4.1MB of image into 5.5MB of text that no browser could cache separately.

I rebuilt it as a static Astro site served from Cloudflare Workers. Content lives in collections with schemas that validate at build time, so a typo in a project's status fails the build rather than rendering. Fonts are self-hosted instead of loaded from Google, which removed two external origins and made an enforced Content Security Policy of `script-src 'self'` possible with no exceptions at all. I wrote eleven decision records into the public repository, each recording the options I rejected alongside the one I chose, because six months from now the decision is the part I will remember and the reasoning is the part I will not.

I built it working with Claude throughout, and I could not have built it alone at my current level. I do not think pretending otherwise would be worth anything. What I brought was the constraints and the discipline to hold to them: check for exposed credentials before every commit, verify a countermeasure by watching it fire rather than by reading it, and write down every error as it happened. Claude followed those and sharpened them. I made every decision and ran every command.

What I took from it was a distinction I had not made before, between a check and a test. A check confirms what you expect. A test can tell you that you are wrong. Almost everything I verified during this build passed and taught me nothing. The few that found something were the ones written so that failure would be visible: a commit hook I tested by planting a fake credential rather than by reading it, a request made over plain HTTP instead of HTTPS, and a contrast measurement on text I had chosen by eye. That last one came back at 1.58 to 1, where the standard for body text asks for at least 4.5 to 1. In plain terms, the grey was close enough to the background that it was barely there. It had already shipped to five pages, it looked fine to me, and neither of us had thought to measure it. By the end of the day the error log had fourteen entries, and most of what it caught surfaced because I read output I expected to be boring.

Live site: [tomokicheung.com](https://tomokicheung.com/)

Source: [github.com/tomokicheung/tomokicheung.com](https://github.com/tomokicheung/tomokicheung.com)
