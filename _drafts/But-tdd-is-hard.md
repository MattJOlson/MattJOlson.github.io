---
layout: post
title: '"But TDD is hard!"'
---

When I [preach the Good News about TDD]({% post_url
2016-05-18-When-to-TDD %}), I hear this a lot. (Mostly I hear it in the
form of "But I _can't_ TDD!", usually with more than one syllable for
"can't", but let's not quibble.) And often, yes, TDD _is_ hard, and it's
not always hard for uplifting gritty inspirational protestant-work-ethic
reasons that will eventually make you a better developer.

# Sometimes, TDD is hard because your build sucks

I'm an ardent continuous-testing fanboy, and sometimes it's hard to get
me to shut up about just how great [NCrunch](http://www.ncrunch.net/) is
for Visual Studio developers. But NCrunch can't handle the full gamut of
weird shit you can do with your VS build -- hell, sometimes _Visual
Studio_ can't handle it, either -- and if that's the case I'm going to
be rebuilding my project every time I run its tests, like a _peasant._

Or worse, I'm going to be offloading them to the CI server, because I
just can't _run_ them locally. Sometimes, heavily-integrated code is
like that.

Or yet _worse_ than that, I might be working on a big ball of C++ mud
with twenty-minute build times in the best-case scenario.

The mitigation here is to try to build unit tests that let you exercise
at least _some_ of what you're writing without rebuilding the world.
It's often _technically_ possible, even if it takes a bunch of
refactoring to carve your own little feature set off into an antiseptic
bubble of at least putative sanity. But it's not necessarily possible
under your tight deadline (particularly if you need to write a _lot_ of
tests to get the code you need to modify into a robust state), or under
your particular political regime.

# Sometimes, TDD is hard because your code sucks

Well, not _your_ code, I'm sure. But we've all seen -- and probably had
to maintain -- god-object bullshit that news up half of its dependencies
in random method calls and has had the other half -- approaching about
_fifty_ of the damn things -- painfully injected into the constructor by
way of the gnarliest explicit DI-container configuration you've ever
seen. Guess what I did at work today?

This is code that's technically _testable_, but it takes you the better
part of _forever_ to actually get it _under_ test. You construct a house
of cards scaffold that you _think_ is going to inject the right data
into the right parts of that eight-hundred-line VB.NET godroutine, but
when you try it you get the most obscure exception you can imagine
(because it's running in a different process, and much gets lost in
translation), and the most productive thing you can manage is hitting
F10 over and over in the debugger until you discover that you've missed
a field in _one_ of the ADO recordsets you stubbed in (but one that'll
cause a similar failure if you include it in the other place).

The mitigation _here_ is a bottle of bourbon. Split it with the guy who
remembers the most about the codebase when your particular demon was
written, and spend some time pairing over the problem if you can manage
it.

But what I'm really trying to say is:

# If TDD is hard, it's because something sucks

Maybe it's your build. Maybe it's your codebase. Maybe it's your design.
(And I write "your" here, but it's probably not something _you_ created
so much as something _you_ got stuck with.)
