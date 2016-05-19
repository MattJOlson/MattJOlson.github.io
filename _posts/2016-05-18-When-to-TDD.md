---
layout: post
title: When to test-drive your code (and when not to)
---

It's awfully presumptuous for me to be writing this. After all, I only
_really_ started test-driving my code a year ago, and even then it was
because I needed to demonstrate fanatical, fundamentalist,
write-no-code-except-to-turn-the-red-bar-green Kent Beck TDD to get a
job. I threw myself into the deep end, got the job (and it's a great
job!), and somewhere along the line realized that red-green-refactor had
incorporated itself into my idea of what constitutes "good enough". So
this is to a not insignificant extent the [zeal of the
convert](http://rationalwiki.org/wiki/Zeal_of_the_convert); let's all
take it with a pillar of salt.

Or maybe let's not. I've worked with a _lot_ of people who claim to
test-drive their code but mostly just let code reviews drive their
tests; for them, unit tests are something you write because your pull
request won't pass review without them, a chore you complete to the
minimum possible bar of effort. And you've got fifteen endorsements for
"TDD" on your LinkedIn profile, because of course you do.

I've worked with even more people who "just don't see what all the fuss
is about". Testing is QA's job, isn't it? They have massive suites of
regression tests that take days to run, that's hardly a practical way to
write code. And what's the point in writing a test if it won't even
_compile?_

> These people often tell me that TDD is an "academic" exercise. I am
> here to tell you that I *crashed and burned* with TDD when I was an
> academic, probably because I was doing it wrong and probably because
> the tooling was way behind the level I currently enjoy. Mainly it was
> because my whole department held it in contempt -- what sort of bold
> academic needs a *safety net* to climb onto the shoulders of giants?
> -- and it's difficult to pursue something, badly, when the people
> who're supposed to be your role models are telling you it's a foolish
> and cowardly waste of time.

Anyway, let's get on with the programme and discover if you really
_don't_ need to test-drive your code.

## TDD to get rapid feedback

Imagine writing code for hours, churning out dozens of methods and
hundreds of lines, until you finally get to a place where your code will
build and run -- and then discovering that it's _all wrong._ You
diligently step through it in the debugger; the NullReferenceExceptions
are easy to find and fix (except when there's no _way_ that reference
could be null, not _here!_), but you find yourself groveling over the
values of locals as they flicker from iteration to loop iteration,
trying to sort signal from noise.

What a nightmare! Good thing it only took me eighteen _years_ of
programming experience to stop doing that on a professional basis.

A decent unit testing framework lets you exercise even the innermost
reaches of your code _as soon as you've written it._ You don't need an
entry point, or a user interface, or a SOA framework to drive the code
that calls into your domain logic -- you just poke the domain code with
a properly-shaped stick and see if it gives you the right kind of oink.
"Hey, does my code actually work?" Find out in five seconds.

Remco Mulder's [NCrunch](http://www.ncrunch.net/) is a minor miracle in
this regard. Remembering to hit ctrl-U, U after fixing up a few lines of
business logic, then waiting for the project to build and your tests to
run, doesn't seem like a hardship until _you've had a piece of code take
care of it for you._ If you're not a .NET partisan, I'm sure you can
still find continuous-testing tools for your platform of choice. You
should use them.

### Maybe don't TDD if you live in a REPL

TDD's biggest advantage, as far as I'm concerned, is that it enables
damn near instant feedback about the state of your code. If you
constantly run and exercise your code in a REPL, maybe you're already
getting instant feedback!

Of course, coding in a REPL and test-driving your code aren't mutually
exclusive. Maybe you nail down boundary conditions or acceptance
criteria with automated tests so you don't have to set them up by hand
every time you change your code, but throw ad-hoc test data at your code
in the REPL when it's easier to do that than to code up the scaffold of
yet another damn test case. Like beer and brisket, REPLs and TDD are two
great tastes that taste great together.

### Definitely don't TDD if your build times are horrifying

I know how it is, I've worked on four gigabytes of C++ codebase too. If
a best-case incremental build takes you ten minutes and touching a
header file means come back tomorrow, you probably won't get much out of
fundamentalist TDD. Maybe you can use a test framework to execute _some_
of your code before the whole ponderous beast is assembled, but at the
_very_ best your step sizes are likely to be a _lot_ longer.

> If you've done tight-loop TDD on a project with full build times
> measured in hours, by all means yell at me on twitter. Better yet,
> blog about it and show me up by posting it for all to see!

## TDD to document your code in a way that cannot lie

The problem with code-level documentation -- or _any_ documentation, for
that matter -- is that it's a pain in the ass to write and rapidly
becomes irrelevant as the code evolves. I've written a ton of wiki doc,
mostly because that was the least bad option. It's hard to write, hard
to find, hard to relate to the code, and requires constant upkeep. Even
then, maybe thirty percent of the people who ought to read it ever will.

Tests work much better as documentation. If you're writing code, you
should already have the tests available to you -- they're in the repo
you checked out, probably in the same project as the code you're working
on. They're easy to find (anything from "Find all references" to `grep`
will do the job), and if they pass they'll tell you exactly how the code
in question behaves.

If you write your tests _first_, you're blessed with not having to
remember all the features you have to document, because you documented
them by test-driving them. You also won't have to remember to document
all the corner cases, because you handled _those_ by test-driving
_them_, too.

### Don't rely entirely on TDD if your docs require bling

If you need flow-charts or UML or Powerpoint to hit your requirements,
TDD isn't your silver bullet.

### Don't count on TDD for documenting an open host

If you want to document your bounded context's interface with the rest
of the big, wide, scary, uncaring world... unit tests aren't gonna cut
it. Probably you've come across something like Swagger or Apiary if you
have an HTTP REST API, and they aren't notably terrible. Perhaps you'll
be able to use [Pacts](https://github.com/realestate-com-au/pact) or
something similar. That sounds nice. Can I come visit?

### Definitely don't TDD if you're a [Real Programmer](http://www.catb.org/jargon/html/R/Real-Programmer.html)

"If it was hard to write, it should be hard to understand!"

Also, tests as documentation will deprive you of the _hilarious fun_ of
comments like:

```
i--; // Add one to i
```

_Also_ also, I hope we never meet. Jerk.

## TDD to write more SOLID code

For all that I'm an ardent advocate of test-driven _development_, I'm
still a bit skeptical about test-driven _design_. Maybe I'll come around
at some point. But either way, test-driving your code makes it more
natural to write code that's
[well-separated](https://en.wikipedia.org/wiki/Single_responsibility_principle),
just because it's easier to test chunks of code that only have to do one
thing. It makes it more natural to write loosely-coupled code, because
if two classes are close collaborators they get _painful_ to unit test
in isolation. You might find yourself tending towards better
command-query separation, because queries are easy to test and commands
are bad enough without having to check for output as well.

[This might sound
familiar!](http://kozmic.net/2012/10/23/ioc-container-solves-a-problem-you-might-not-have-but-its-a-nice-problem-to-have/)

### Don't TDD if you don't know when to stop

David Heinemeier-Hansson coined the term [Test-Induced Design
Damage](http://david.heinemeierhansson.com/2014/test-induced-design-damage.html).
We should rightly fear TIDD Syndrome, where every collaborator can be
mocked out by an interface (you _need_ an interface, because you'll need
to mock it for tests!) and every operation is performed by instantiating
a class that satisfies a particular interface that provides a particular
service. I'm exaggerating, but holy shit, not by much.

> One ominous sign of TIDD is when you ask yourself, or your colleague,
> or Stack Overflow: "How do I test my DI container configuration?" At
> that point you should probably just set your codebase on fire before
> it infects the whole city.

If you find yourself with many interlocking patterns of mutable and
interdependent state -- in DDD terms, that means a thundering herd of
entities that can't _not_ be in the same aggregate -- you might have a
problem. If you find that you have to inject seven or eight different
mock objects into a single class in order to test one of its public
methods, that class might be doing too much. If you keep adding stuff to
a single kitchen-sink interface because you don't want to mock up _yet
another goddamn object_, you might consider taking a deep breath and a
step back. All the pain that "test-driven development" is causing you
just might be a suggestion to rethink your design.

I'd offer you a solution, but I don't have to, because [Mark Seeman has
already done a damn good
job](https://app.pluralsight.com/library/courses/fsharp-test-driven-development/table-of-contents)
on PluralSight. It turns out that, rather than depending upon a complex
web of invariants between various chunks of mutable state, it's a lot
easier if you can make the mutable-state part go away.

And finally, we get to:

## TDD to do your fucking job

Yes, _obviously_ it's possible to do your job without test-driving your
code. I've done it for well over a decade, and it was more trouble than
it had to be (although I was mostly writing C and C++, so maybe I'm
wrong about that -- see "compile times", above). But if you give a shit,
if you take some pride in what you do, you don't like getting test-case
fails back from QA or having some smug asshole (or dear colleague) point
out obvious bugs in code review. You want to push your code and raise a
pull request in unshakeable certainty that you're going to bathe in the
admiration of everyone who reads it, and that when _your_ ticket hits QA
it'll sail through in _minutes_.

Since I started religiously (yeah, the term is indicative, sorry I'm not
sorry) test-driving my code, I tend to forget to actually _test_ it by
hand. I don't really bother firing up Postman and verifying the ticket's
acceptance criteria.

Maybe one time in fifteen I miss a spot and I get rapped across the
knuckles by QA for my negligence. That just means I need to write better
tests. With the panoply of test-automation frameworks we have available,
it's ridiculous that anyone should have to fiddle-fuck HTTP request
parameters or hand-hack JSON payloads to check my work against the
acceptance criteria that we'd originally written into the ticket. That's
busy-work at _best_.

### Don't TDD if you enjoy goldbricking

"Oh, I thought I had all the acceptance criteria covered, I guess I
missed that one." Shit, now you'll have to fix that one thing and put it
back into code review and wait until QA has time to pick it up again.
That ought to give you plenty of time for Facebook.

Also, I hope we never meet. Jerk.

### *Definitely* TDD if you enjoy goldbricking a little too much

If you give me a clear board with no new tasks to pick up, I'll find
myself something to do. There's always code that needs cleaned up, or a
utility library that should probably be documented so we can quit
reinventing its functionality every time we write up a test suite for a
new project. I'll get there, eventually. Might take a minute to check
Twitter first. Shit, am I out of coffee?

If you show me a test that's red, I turn into a _missile._ I'll
cheerfully spend the next four hours tracking down that end-to-end test
failure to that submodule update that got applied _here_ but not over
_there_, and I don't care _what_ just happened in free agency. I'll
catch up on the train home, nbd, I have _work_ to do.

Red-green-refactor hits the same spot for me. I can't let go of a
failing test, and once I get it to pass I can't usually bring myself to
push that commit until I've refactored it to not suck. I expect you're
the same way, because this is (broadly speaking) how slot machines and
MMOs work.

## Appendix: TDD your changes to legacy code

"Get code under test before refactoring" -- I really don't have to
explain this, do I? Granted, this is more a matter of test-_first_
development than test-_driven_ development, because you're starting out
by nailing down the behaviour of the big ball of mud you need to modify
rather than writing failing tests to describe its _new_ behaviour, but
it's far better than blindly messing with existing code and hoping it
all works out for the best.

### Don't TDD your changes if it's easier to regression-test

Sometimes it's straightforward to run an automated regression test suite
against your codebase, but breaking enough dependencies to get the
particular module you're hacking on properly under test would take
weeks. If you don't have weeks (or, maybe, if you _do_ have weeks but
nobody's likely to benefit from the fruits of your labour), labouring to
inject a zillion dependency interfaces just so you can abuse your
favourite mocking library is _not_ the most productive use of your time.

Fiddle-fucking around with partial mocks and argument matching and so on
can be a lot of fun, in that peculiar complexity-worshipping way we tend
to enjoy, but let's not underestimate the power of throwing a
brute-force regression suite at a piece of legacy code on a modern,
high-horsepower computer. Sometimes it takes less clock time than all
the reflection your mocking framework needs to get itself bootstrapped.
