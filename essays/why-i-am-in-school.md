---
layout: essay
type: essay
title: "The bug that showed me why I am in school"
date: 2026-09-08
published: true
labels:
  - Web Development
  - Debugging
  - Cloudflare
  - Learning
---

## The gallery broke overnight

I check the websites I have built every morning. It takes two minutes and it is how I found this.

One morning the services gallery on my first client's site was broken. The cards were supposed to slide left to right as you scrolled. Instead they were stacked vertically, top to bottom, and the images inside them were gone. A small marker that travels along a rail through the section had disappeared too.

Nothing had been deployed since the day before. I had not touched the file. Opening the same page on my own machine looked completely normal.

## I did not know what I was looking at

My first guess was that the images were misaligned and something in the CSS had broken. That is what it looked like. It never occurred to me that the cause might have nothing to do with my code at all.

So I asked Claude, and I was honest that I did not know what was happening. We worked through it together. The first theory was the CSS. That was wrong. The second theory was also wrong, and at one point I was talked out of the correct answer. About half an hour went by before either of us suggested opening the browser console and reading it.

When I did, the console looked empty. It was not. Chrome hides messages behind a severity filter, and errors can sit behind a small "N hidden" counter that is easy to scroll past. Once I switched it to show all levels, the error was right there.

## The cause was something I did not write

A script had been blocked by my own [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy).

A Content Security Policy is an HTTP header that tells the browser which sources it is allowed to load code from. It is a security measure. If someone injects a malicious script into your page, a strict policy means the browser refuses to run it. I had added one a few days earlier by reading through my HTML, listing every domain the page loads something from, and allowing exactly those.

```
script-src 'self' 'unsafe-inline' https://cdnjs.cloudflare.com https://cdn.jsdelivr.net;
```

That list is correct for the file. The file is not the whole page.

The site is served through Cloudflare, and Cloudflare adds its own analytics script to pages at the edge. It is not in my HTML. It does not appear in my editor, it does not show up if I search the repository, and it does not exist on my computer. It is added on the way out to the visitor. My policy blocked it because I did not know it was there.

Then it got worse in a way I had caused myself. Weeks earlier I had written a small watchdog whose job was to notice if the animation library failed to load and drop the page into a plain readable version instead of showing a blank screen. The watchdog saw a script fail. It could not tell which one. It assumed the animation library was gone and did exactly what I had told it to do. Every symptom I spent half an hour chasing was my own fallback working correctly, triggered by the wrong script.

## What I actually learned

The fix was one line. Adding Cloudflare's domain to the policy took seconds once I understood the problem. Understanding the problem was the hard part, and I could not have done it on my own.

That is the thing worth writing down. Up to that point I had been treating web development as a smaller subject than it is. You describe what you want, you get an HTML file, you deploy it, it works. That process had worked well enough that I had not noticed how much I was not seeing. Headers, edge behaviour, what a platform injects into your page after you stop looking at it, where API keys live and who can read them, what happens when a third-party script you did not write fails. None of that is in the file.

I could not have debugged this by reading generated code, because I did not understand the code well enough to know what could go wrong with it. That distinction is the whole thing. Producing something that works and understanding something well enough to fix it when it stops working are not the same skill, and only one of them survives contact with a real client.

This is why I am in school rather than only building things. I want the fundamentals underneath the tools, so that the next time something breaks I have a better first guess than "the images look misaligned." I still do not fully understand everything that happened that morning. But I know what I am missing now, which is a considerably better position than not knowing.
