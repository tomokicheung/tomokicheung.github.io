---
layout: essay
type: essay
title: "The script I never wrote broke my client's website"
date: 2026-09-08
published: true
labels:
  - Web Development
  - Debugging
  - Cloudflare
  - Security
---

## A gallery that stopped being a gallery

Every morning I open the websites I have built and look at them. It is a boring habit and I recommend it. One morning in September I opened my first client's site and the services gallery was wrong. Cards that were supposed to slide left to right as you scrolled were stacked vertically instead. The images inside them were gone. A small hibiscus marker that travels along a rail as you move through the section had vanished too.

The site had been live for days. Nothing had been deployed since. I had not touched the file. My local copy looked perfect.

## Three theories, all wrong

My first thought was that a CSS rule had broken and the cards had lost their layout. That is what it looked like, and it is the kind of problem I had caused before. I went looking for a selector that no longer matched anything.

That was wrong, and so were the two theories after it. I want to be specific about the wasted time because it is the part of this story I actually learned from. I spent close to half an hour reasoning about what could produce that symptom, and I argued myself out of the correct answer at least once along the way. What I had not done was open the browser console and read it.

When I finally did, the console looked clean. It was not. Chrome's console has a filter for message severity, and by default it can hide errors behind a small "N hidden" counter that is easy to scroll past. Once I set it to show all levels, the actual error was sitting there, and it took about fifteen seconds to understand.

## What the console actually said

A script had been blocked by my own Content Security Policy.

A [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) is an HTTP header that tells the browser which sources it is allowed to load code from. It is a good idea. If someone manages to inject a malicious script into your page, a strict policy means the browser refuses to run it. I had written one for this site a few days earlier, and I wrote it the obvious way: I read through the HTML, listed every domain the page loads something from, and allowed exactly those.

That list is complete, as far as the file is concerned. The problem is that the file is not the whole page.

The site is served through Cloudflare, and Cloudflare injects its own analytics beacon into pages at the edge. That script is not in my HTML. It never appears in my editor, it never shows up in a search of the repository, and it does not exist on my machine. It is added on the way out to the visitor. So my policy, written carefully from a file that does not mention it, blocked it.

## My safety net caught the wrong fall

Blocking an analytics beacon should be harmless. It was not, and the reason is the part I found most interesting.

Weeks earlier I had written a small watchdog for this site. Its job was to notice if the animation library failed to load from its CDN and, if so, quietly drop the page into a readable static version rather than leaving a visitor staring at a blank screen. The gallery only animates because of that library, so without it the cards have nothing to position them.

The watchdog saw a script fail. It could not tell which one. It concluded the animation library was gone and did exactly what I had told it to do. Every symptom I spent half an hour investigating was my own fallback working correctly, triggered by the wrong script.

That is a strange thing to be pleased about, but I am. The failsafe was written on a quiet afternoon and did nothing visible until the day it mattered, and when it fired it produced a degraded page instead of a broken one. The contact form still worked the whole time.

## What I check now

Three things changed in how I ship.

I no longer trust localhost to tell me a site is fine. Cloudflare is not in front of my laptop, so none of the headers, injected scripts, or edge behaviour that produced this bug exist locally. When something works in one environment and not the other, that gap is now the first place I look rather than the last.

I ship a new Content Security Policy in `Content-Security-Policy-Report-Only` mode first, watch the console for a day, and only then enforce it. A wrong policy does not throw an error page. It fails silently and takes something with it.

And I read the console before forming a theory. I know how obvious that sounds. I still did it in the wrong order, and the cost was thirty minutes of confident reasoning that a single line of text ended instantly.

The part I keep coming back to is that every individual piece here was correct. The policy was well formed. The watchdog behaved as designed. The platform did what it advertises. The failure lived entirely in the space between them, and none of the pieces could see that space from where it stood. That is the difference between writing code that works and building a system that works, and it is the reason I want to keep doing this.
