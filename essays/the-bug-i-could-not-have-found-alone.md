---
layout: essay
type: essay
title: "Understanding the websites I build"
date: 2026-09-08
published: true
labels:
  - Software Engineering
  - Learning
  - Web Development
  - Security
---

## Building with LLMs

Over the past several months, I've built and launched a handful of websites, including one for a paying client. Large language models helped me turn ideas into working sites, but my ability to produce them was ahead of my understanding of the code.

I could explain the design, intended behavior, and business requirements. I couldn't always explain how the implementation worked. With a client depending on my work, I needed to address that gap.

## What my security reviews covered

I paid attention to exposed API keys, credentials, and the risks of publishing code in public repositories. I asked for security reviews and questioned suggestions that looked wrong.

My reviews were still limited by what I knew to check. I could ask whether I'd exposed a secret, but I was less prepared to evaluate interactions between browser behavior, hosting features, and security settings. A working page wasn't enough to confirm that I understood those interactions.

## The gallery failure

About a week after launching my client's site, I found a broken services gallery during my morning check. Cards intended to move horizontally were stacked vertically, and images were missing. The page still looked normal on my machine, and my most recent deployment had been the previous day.

I initially suspected CSS because the visible problem was the layout. While troubleshooting with Claude, I checked the browser console and found a Content Security Policy error blocking a script.

I'd added the CSP a few days earlier. It controls which resources the browser can load and execute. I had configured it around resources referenced in my HTML without fully accounting for changes Cloudflare could make when serving the site, including injecting scripts.

![Browser console showing a Content Security Policy blocking Cloudflare's beacon script](../img/essay/console-error.png)

The console showed Cloudflare's beacon script being blocked and a separate message from the site's fallback reporting a script-loading failure.

I changed the configuration that morning, confirmed that the gallery worked again, and informed the client.

The exact cause still needs qualification. The blocked script and the gallery failure appeared during the same investigation, but I hadn't established how they were connected. Restoring the gallery confirmed that it worked again; it didn't establish a complete diagnosis.

## What I need to understand better

The incident exposed a limitation in how I reviewed my work. I had focused on the files in my editor without fully accounting for how the hosting configuration and browser affected the delivered page.

That is part of why I'm pursuing a computer science degree. I want to understand the systems behind what I build so I can evaluate generated code, investigate failures, and explain my decisions. Coursework will support that, but I'll also need to apply it to real projects.

I'll continue using LLMs. They've helped me build projects beyond what I could have completed independently at this stage. My responsibility is to understand and verify the work I deliver, including being clear about what I haven't yet established.
