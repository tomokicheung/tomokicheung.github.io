---
layout: essay
type: essay
title: "Coding standards, one week in"
# All dates must be YYYY-MM-DD format!
date: 2026-09-23
published: true
labels:
  - Software Engineering
  - Coding Standards
  - ESLint
---

Before taking ICS 314, I didn't really have a coding standard. What I had were habits that I slowly developed while taking introductory programming courses and watching how other people wrote code through YouTube demonstrations. Before using ESLint, I'd write control statements without spaces after keywords such as if, for, or while (for example, `if()`, `for()`, and `while()`). I'd indent using whatever my tab key produced, and I'd write comments like `//comment` instead of `// comment`. The first time I ran ESLint on my own code, most of those habits came back as errors despite the program running completely fine.

What I learned from practicing with ESLint is that these errors are tied to specific rules. For example, `keyword-spacing` is why writing something like `if()` produces a style error, while `spaced-comment` is why `//comment` fails. Before this class, I probably would have looked at those differences as minor formatting preferences. Now I understand that a coding standard creates consistency across a project, especially when multiple people might eventually read or work on the same code.

## Learning from the Baby Bieber WOD

While working on the `baby-bieber` practice WOD on Monday, September 21, my first lint run reported a handful of errors. One that keeps getting me is `eol-last`, which means I left the file without a newline at the end. It's a small mistake, and it doesn't stop the program from running, but ESLint still catches it every time. Repeatedly seeing errors like this has started making me more aware of how I format my code before I even run ESLint.

This is where I agree that coding standards can help someone learn a programming language. I think ESLint does more than tell me whether my code runs. It forces me to notice details that I probably would have ignored otherwise. At the same time, I don't think passing ESLint automatically means the code itself is good. A program can follow every formatting rule and still have incorrect logic, produce the wrong output, or be written in a confusing way. ESLint seems to check one part of code quality, but testing and actually understanding the program are still needed for me to do.

Before ESLint, I mostly focused on making sure my code ran and produced the appropriate output. Now I also try to ask myself whether it's written the way it should be, given the standards and constraints of the project. I think passing ESLint doesn't exactly prove that code is good, but understanding why it doesn't pass is already making me more careful. With repetition, I expect that writing code in the style ESLint expects will eventually become more natural instead of something I have to think about every time.

*AI use: I used ChatGPT for grammar, wording, and structural feedback while revising this essay. The experiences, technical details, and conclusions discussed are my own.*
