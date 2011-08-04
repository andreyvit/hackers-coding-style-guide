---
layout: page
supertitle: "2011 Hacker's Coding Style Guide"
superlink: "./"
title: "Whitespace & Indentation"
comments: true
sharing: true
footer: true
---

Avoid tabs, use spaces. Why? [Reasoning is here](why-tabs-should-be-avoided.html).

Indent with 4 spaces by default, unless the language has another convention. (Idiomatic CoffeeScript should use 2 spaces for indentation. Ada prefers 3 spaces. Other languages either want 4 spaces or don't care.)

Never, ever leave trailing whitespace. In particular, make sure your empty lines are truly empty. Some editors can be configured to strip trailing whitespace on save. Alternatively, you can run [an external tool like `white`](http://github.com/andreyvit/white) before committing.

Every file must end with an empty line. Another way to say this is that every line must end with a new-line character. (Some languages like C++ even have undefined behavior when source files don't have a trailing new line.)

Git indicates whitespace errors when committing or diffing. Listen to what it says and correct it promptly.

If you are inclined to fix whitespace in an already committed code and cannot edit those commits directly, please put whitespace changes into a separate commit.
