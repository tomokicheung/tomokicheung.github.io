---
layout: project
type: project
image: img/pacific/pacific-square.png
title: "Pacific Consulting Hawaiʻi"
date: 2026-05-01
published: true
labels:
  - Web Development
  - Cloudflare
  - Internationalization
  - Client Work
summary: "Migrated a Honolulu events and logistics company off Shopify to a bilingual static site, keeping the same domain with no downtime."
---

Pacific Consulting Hawaiʻi is a Honolulu events and logistics company. They plan events, staff crews, run trucking, and handle inter-island freight. It is a services business with no products to sell. When they came to me, their website was running on Shopify, which meant they were paying a monthly ecommerce platform fee to operate a storefront that had never sold anything. What they actually needed was a site that explained five services clearly and moved a visitor to a contact form, in English and in Japanese, since a meaningful share of their clients are Japanese-speaking.

I was the sole developer on the project. I rebuilt the site as a static build served through Cloudflare, keeping their existing domain so their web address never changed and there was no downtime during the cutover. Rather than maintain two parallel sites, I built a single codebase with an internationalization layer and a language toggle, so English and Japanese content live side by side and stay in sync. The contact form runs through Formspree, which removed the need for a backend entirely. I handled DNS, TLS, and the security headers on the production domain, and wrote a migration runbook and plain-language handoff documentation so the client knows where every account lives and who to call.

The most useful thing I learned came from breaking it. After deploy, the site dropped into a degraded state that had not appeared anywhere in local testing. The cause was a Content-Security-Policy header I had written correctly in isolation. It blocked a script the hosting platform injects at the edge, which in turn tripped a watchdog. Two lessons stuck. The first is that localhost and production are different environments, and a configuration that is correct on its own can still be wrong once the platform adds its own resources to the page. Verification has to happen after deployment, not only before it. The second is narrower and I keep relearning it: read the actual console error before forming a theory. I spent longer reasoning about what might be wrong than it took to find out what was wrong.

Live site: [pacificconsultinghawaii.com](https://pacificconsultinghawaii.com/)