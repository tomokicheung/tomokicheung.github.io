---
layout: project
type: project
image: img/tomokicheung/tomokicheung-square.png
banner: img/banners/about-1600x800.jpg
title: "tomokicheung.com"
date: 2026-09-09
published: true
labels:
  - Web Development
  - Astro
  - Cloudflare Workers
  - TypeScript
  - Web Security
summary: "My personal site showcasing client work, writing, and projects, built with Astro."
---

tomokicheung.com is my personal site, showcasing my client work, writing, and projects under my own domain. I started with a single HTML file I had worked on earlier in the year and rebuilt it to make the content easier to organize, update, and maintain.

The site uses Astro and is deployed through Cloudflare Workers. Shared layouts keep navigation and styling consistent across pages, while content collections check entries for missing or invalid information during the build. Fonts are self-hosted, and a Content Security Policy restricts scripts to the site's own origin. I documented the technical choices and alternatives considered so I could revisit the reasoning behind them.

I worked with Claude throughout the project. At my current level, I could not have completed the same build independently. I set the requirements, reviewed proposed changes, made the final decisions, and ran the commands. The process included checking for exposed credentials before commits, testing security controls, and recording errors and their resolutions.

The build helped me become more deliberate about reviewing changes. In one instance, Claude provided an updated file based on an older version. Replacing my local file would have removed navigation and accessibility changes I had already made. We caught the mismatch before applying it and adjusted the process to make targeted edits against the current file.

I kept a build runbook documenting technical decisions, problems encountered, and their resolutions. Those notes explain the reasoning behind changes and what to check next time. The site gives me a place to share my work, and the documentation gives me a process to revisit and improve as I continue building.

Live site: <a href="https://tomokicheung.com/" target="_blank" rel="noopener noreferrer">tomokicheung.com</a>

Source: <a href="https://github.com/tomokicheung/tomokicheung.com" target="_blank" rel="noopener noreferrer">github.com/tomokicheung/tomokicheung.com</a>
