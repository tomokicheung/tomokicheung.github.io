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
summary: "My personal site showcasing client work, writing, and projects, built with Astro."
---

tomokicheung.com is my personal site, bringing together my client work, writing, and projects under my own domain. I started with a single HTML file I had worked on earlier in the year and rebuilt it to make the content easier to organize, update, and maintain.

The site uses Astro and is deployed through Cloudflare Workers. Shared layouts keep navigation and styling consistent across pages, while content collections check entries for missing or invalid information during the build. Fonts are self-hosted, and a Content Security Policy restricts scripts to the site's own origin. I documented the technical choices and alternatives considered so I could return to the reasoning behind them.

I worked with Claude throughout the project. At my current level, I could not have completed the same build independently. I set the requirements, reviewed proposed changes, made the final decisions, and ran the commands. The process included checking for exposed credentials before commits, testing security controls, and recording errors and their resolutions.

The build helped me become more deliberate about reviewing changes and testing the result. In one instance, Claude provided an updated file based on an older version. Replacing my local file would have removed navigation and accessibility changes I had already made. We caught the mismatch before applying it and adjusted the process to make targeted edits against the current file.

An accessibility check also found that some text was too close in color to its background. It looked acceptable to me, but the contrast was below accessibility requirements across several pages. I corrected the text colors and separated them from colors used for decorative lines so they could be adjusted independently.

I recorded these problems and their resolutions in the build runbook. Alongside the technical decisions, those notes explain what went wrong, how we found it, and what to check next time. The site gives me a place to share my work, and the documentation gives me a process to revisit and improve as I continue building.

Live site: [tomokicheung.com](https://tomokicheung.com/)

Source: [github.com/tomokicheung/tomokicheung.com](https://github.com/tomokicheung/tomokicheung.com)
