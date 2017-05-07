---
layout: post
title: Code aesthetics
---

Let's talk about the aesthetics of code.

> Must we?
>
> Oh shit, I'm in a Socratic dialogue again, aren't I.

Yep. Play your role and we'll be out of here in no time.

So. What makes for elegant code? Code that looks good?

> Who cares, as long as it works?

Write a lot of machine code, hmm? Or alternately, lambda calculus, or
Turing-machine tapes?

> Those are ridiculous edge cases. Pick a normal language, like Java. If
> the code works, it works. Users don't care how you formatted it.

Formatting's an interesting part of code aesthetics, but you're right.
It's not for users, it's for other developers--

> --where "other developers" could mean "you in three months", right?

You're getting good at this.

So yeah, stuff like chopping up function-call argument lists when they
get too long. I think most people would agree that a 250-character
method call with eleven named parameters should be broken up, with one
parameter per line, but if you're only calling a method with two
parameters they can probably stay on the same line.

> Eleven named parameters? That's just awful. ...oh!

Now we're getting to the meat of the matter. An aesthetic for code isn't
just something that gets you internet mad if you see someone mixing tabs
and spaces, it's an internal compass -- maybe more like a Geiger counter
-- that warns you when you're working on (or writing!) bad code.

> Okay, I can see where you're going, but again: Who cares, if it works?

Whoever has to maintain it, update it, bring it into compliance with the
latest RFP demands it has to meet, or debug that weird memory leak you
just noticed when you changed logging frameworks. Ugly code that's
adequate is acceptable until it stops being adequate.

> Pithy.
