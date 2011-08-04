---
layout: page
supertitle: "2011 Hacker's Coding Style Guide"
superlink: "./"
title: "Good Code-P?"
comments: true
sharing: true
footer: true
---

Please target a human being, not a computer. Imagine yourself explaining your code to another person. What can you do to make it easier to understand?

The code should be telling a story. Like any good storytelling, writing code requires focusing on some specific details and omitting the other ones. The way you omit details in a computer program is by abstracting them away as functions and classes.

This section gives the general guiding principles behind all other conventions in this guide.


## Good Code Is…

**Easy to read:** nicely formatted, neatly organized, strikes a right balance between conciseness and verbosity.

**Easy to follow:** uses inversion of control and dynamic capabilities responsibly. Which means, it certainly should use them where appropriate, but the result shouldn't be a mess.

**Easy to reason about:** broken down into modules (files, classes, functions) in a way that makes them easy to analyze. It should be nearly obvious that a module works as advertised just by looking at it individually. (An exception is algorithmic code like parsers and data structures — these one should still be inspectable individually, but you can't really make them so obviously correct.)

**Idiomatic:** uses/follows common practices, conventions and idioms, avoids unjustified surprising ways to do usual things.

**Blends in:** does not redefine the platform with a set of unjustified helpers. This may be hard to understand until you do a certain number of projects. When you go back to your project in a year, you will find most of your helpers lame (because the platform has since improved, and you've also found shiny new ways to do old stuff), and it won't be any pleasure to maitain the code that uses them.

**Avoids maintenance nightmares:** while extensive future-proofing is wrong (and you can never tell which direction you will be going a year from now), things that are known to make maintenance harder should be avoided. Stuff like CSS specificity mess, getter chains (`a.getB().getC().doFoo()`), and using duplicate names for unrelated things in languages with no reliable refactoring tools.

**Commented where comment is due,** only if you cannot express the same by better naming or code reorganization. Appropriate cases are: borrowed code (include a URL), bug workarounds (describe the bug), algorithmic complexity, rationales for untrivial choices (would someone ask why you did it this way?), unobvious tradeoffs and other why's and wtf's.


## Coding Tips

How to design your code so that it's easy to read and reason about:

Keep your modules **focused on one task** (can you describe the responsibilities of your class/module in a single short sentence?) — also known as “high cohesion”.

Keep **intermodule relationships and communications limited** (does your module talk to 1 or 10 other modules? which other modules can break it?) — also known as “low coupling”.

Use **helpful names** and method signatures that **accurately describe the contracts** (can this method ever return null? can it fail? what does it do when it fails?)

Above all else, **keep the state simple**. Make your fields immutable where possible. Make their lifetimes obvious (do they contain a meaningful value all the time? only when the view is on screen? only when the moon is full and the weekday is at least Wednesday?) Prefer common lifetime idioms (like lazy initialization and transparent caching) over complex customized ones.

**Code defensively.** An error in one module shouldn't silently mess up the state of another module. It's ok to do nonsense in reply to a garbage input, but it's not ok to silently end up in a garbage state (at least in a debug version). Complain quickly and loudly, assert and crash if your project allows it, log otherwise. Being able to guarantee the state of each module is key to being able to understand the state of the entire application.

