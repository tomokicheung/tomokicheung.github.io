---
layout: essay
type: essay
title: "The bug I could not have found alone"
date: 2026-09-08
published: true
labels:
  - Software Engineering
  - Learning
  - Web Development
  - Security
---

## Building faster than I was learning

Over the past several months I have built and shipped a handful of real websites, including one for a paying client, working alongside large language models the entire time. It worked. That is the part worth saying plainly, because a lot of writing on this subject starts by arguing that it does not.

What I had was direction. I knew what I wanted a site to do, how it should feel to use, what the business behind it actually needed. What I did not have, and did not notice I was missing for a while, was the ability to keep up with the code I was shipping. Somewhere in the middle of those projects the gap opened up. I could still explain what a page was supposed to do. I could no longer explain how it did it.

That is an uncomfortable position to be in when someone else's business is running on the result.

## The parts I did watch

I want to be fair to myself here, because I was not careless about it.

I knew that a public repository is public, and that anything committed to one is effectively permanent. I asked for security reviews on the projects I worked on and pushed back when something looked wrong. I was deliberate about API keys and credentials, and about not exposing anything that would let someone act on my account or a client's. Those are the failure modes people write articles about, and I was watching for them.

The problem is that those are the failures you can look for. You know to check whether a key is in the frontend because someone told you to check. The failures that worried me over the summer were the ones I would not know to look for, because knowing to look for them requires understanding the system well enough to imagine how it breaks. I did not have that. I had a working site and a strong sense that "working" and "sound" are not the same word.

## The morning it stopped being theoretical

I check the websites I have built every morning. It takes two minutes.

About a week after launching my client's site, the services gallery was broken. Cards that were supposed to slide left to right as you scrolled were stacked vertically instead, and the images inside them were gone. Nothing had been deployed since the day before. Opening the same page on my own machine looked completely normal.

My first guess was that the images were misaligned and something in the CSS had broken. That is what it looked like. It did not occur to me that the cause might have nothing to do with my code at all, because I did not know that was a category of problem that existed.

It was not the CSS. A script had been blocked by a [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) I had added a few days earlier. A Content Security Policy is an HTTP header that tells the browser which sources it may load code from, and I had written mine the obvious way: read through the HTML, list every domain the page loads something from, allow exactly those.

```
script-src 'self' 'unsafe-inline' https://cdnjs.cloudflare.com https://cdn.jsdelivr.net;
```

That list is correct for the file. The file is not the whole page. The site is served through Cloudflare, and Cloudflare adds its own analytics script to pages at the edge. It is not in my HTML, it does not appear in my editor, and it does not exist on my computer. It is added on the way out to the visitor, and my policy blocked it because I did not know it was there.

I found it by asking Claude to diagnose it and working through the possibilities until we opened the browser console and read the error, which took a fraction of the time the guessing had. I fixed it that morning, then told the client what had happened rather than waiting for them to notice.

## Why I am in school

The fix was one line. Understanding why the line was needed is the part I could not have arrived at on my own, and that is the whole point.

This is what I had been uneasy about all summer, arriving in a form I could not talk myself out of. It was not a bug in something I wrote. It was a bug in the space between my code, a platform's behaviour, and a security header I had added without fully understanding what it governed. Nothing in the file would have told me. No audit I knew how to ask for would have caught it, because I did not know the question.

I am pursuing a computer science degree because that is the gap it closes. Not the syntax, which I can already get from a model faster than I could type it. The fundamentals underneath: how systems compose, what happens at the boundaries between things you wrote and things you did not, why a piece of infrastructure behaves differently in production than on your laptop. Producing something that works and understanding it well enough to fix it when it stops working are not the same skill, and only one of them survives contact with a real client.

I am not going to stop building with these tools. They are genuinely useful and I would be worse off without them. But I would rather be the person who can read what comes back. I still do not fully understand everything that happened that morning, and I intend to keep chipping away at that. Knowing specifically what I am missing is a considerably better position than not knowing.
