---
layout: post
title: That Practice Needs Practice
---

## tl;dr Learn the practices of your shit, not just the techniques

Those tasks you think are stupid wastes of your time? Maybe think of
them as _practices_, rather than _stupid waste-of-time tasks_.

## Okay, we've lost the lazy fuckers
I bet you've heard something like this before, maybe even from your own
mouth-parts:

> Oh, come on, TDD? That stuff doesn't work! It sounds great in theory,
> but in practice it's a waste of time!

Feel free to substitute "pair programming", or "planning poker", or
"sprint retrospectives", or "event storming", or whatever else you like
for "TDD". I'm pretty sure we've all been there.

And it's not like we're _lying_ when we make these claims, either. As an
example, I got _very_ into Kent Beck's TDD book -- and, as a follow-on,
_eXtreme Programming Explained_ -- around the beginning of 2004, when I
was about a semester and a half into grad school. I threw myself into
unit testing and conned -- er, _recruited_ -- a lab-mate into a couple
of pair-programming sessions.

I gave up after two weeks. "This stuff might work in _industry_, but
it's just _not suitable_ for academia."

## Test-Driven Development

Look at that second word, the one right after the hyphen. "_Driven_".

There's a thundering herd of books, courses, blog posts, and consultants
out there to teach you how to write unit tests, how to write acceptance
tests, and how to attempt to avoid writing integration tests.
Given-When-Then! Arrange-Act-Assert! Dependency injection! Mocks and
stubs! We've got this subject nailed to the _wall_.

I know _dozens_ of developers who write incredibly sophisticated,
technically adept test suites. I know maybe _two_ who actually drive
their development with tests.

> Tests *first?* That's a waste of time! I don't even know what to test
> if I write my tests first!

My good fortune is that I learned TDD -- dogmatic, Kent Beck-style TDD
-- not in order to up my game as a developer, not in order to add bling
to my LinkedIn profile, but because I needed a job. I was eight months
unemployed, and the company's recruiter flat-out told me I didn't have
the skills they were looking for in a developer. Somehow I got a coding
interview anyway. In C#. Which I'd spent the last decade or more writing
off as "Microsoft's bastard version of Java, which by the way I also
hate".

I spent three days with my twelve-year-old copy of _TDD By Example_ more
or less glued to my hand. I didn't have _time_ to learn about partial
mocks or SpecFlow or IOC containers. All I learned was:

* Red. Green. Refactor. Repeat.
* Take small steps if you feel uneasy. Take bigger steps if you feel
confident.

I kicked the _shit_ out of the [String Calculator
kata](http://osherove.com/tdd-kata-1/) in a language I'd barely started
to learn. I had to stop and ask my interviewers how to tokenize a
string. I had to stop and ask, after fucking it up three times, how to
write a lambda. They stopped me early because they'd decided to hire me.

I've never gone back. I just don't _write_ code any more unless I've
figured out how to make that test bar turn red. It's a bit limiting
around REST APIs, but I'm okay with that.

Do I sound like I think I was hot shit when I took that interview? I
wasn't. I took a routine question about dependency injection and
_mangled_ it instead of having the self-confidence to say "I have no
idea". I watched them roll their eyes at each other as I finished my
sentence and nearly crapped my drawers. But:

* Red. Green. Refactor.
* Take small steps.

### Why does that work?

Red-green-refactor is the _practice_ of TDD. It's not an implementation
detail, like constructor injection or pattern-matching in FakeItEasy.
Those are neat tools to have in your kit, but if you're writing your
tests at the end of the ticket they're not going to help you. It's not
about _tools_, it's about _practice_.

If you watch your tests _fail_ when you _know_ that the feature they're
testing isn't there, then watch them _pass_ when you've just implemented
the feature, you know that your tests _work_. (At least in the case
where you didn't have the feature at _all_ before. Maybe there's a bug
in your code that your tests didn't catch! I guess you'll have to write
a test to tickle that bug before you fix it. Red. Green. Refactor.)

If you have to write a _failing test_ before you're "allowed" to write
more feature code, it's harder to fall into the trap of writing code
that "I know we're going to need for the next ticket". Leave that shit
for the next ticket and do your job, which is coding up _this_ ticket.

If you have to write a _failing test_ for each new behaviour you
introduce to the codebase, then you've _de dicto_ written some
_executable documentation_ for each new feature you've implemented. To
me, this result of TDD is better than all the rest combined; you could
write your tests, run them _twice_ (once for red, once for green), and
then ignore them until the end of time, and I'd _still_ rather work on
your code than the output of dozens of code ninjas who "finished a
ticket" and then had to go back and remember what tests they had to
write.

More to the last point: Test-first code reads differently. If you wrote
your tests at the _end_ of your development effort, I'll be able to
tell, and I'll have to spend a good two-thirds of my code review poring
over the whole goddamn diff and trying to figure out if you covered
everything that needed to be tested. If you wrote your tests before
they'd even _compile_, that's _also_ obvious, and I'll review your code
by reviewing your tests and then style-checking your feature code in,
like, twenty minutes. Not because I'm a full-zoot high-octane code
reviewer, but because your test-first tests will make it _boringly
obvious_ that your code is correct.

(Oh yeah, there's supposed to be stuff here about dependency injection
and loose coupling and how all that falls out of TDD, but I find that if
your codebase has a DI container someone's going to yell at you if you
new shit up in your constructors whether you have tests or not. Test
driven _architecture_ is a practice I have yet to discover, so I'm not
going to write about it. Yet.)

### What's the point?

I knew _shit-all_ about the technical intricacies of TDD when I
interviewed. It took me a month and a half to get comfortable with DI
and mocking frameworks. (Part of that's probably down to the fact that
the first mocks I wrote were partial mocks for Angular services, but
that's a rant for a different time.) But I picked up on the _practices_
of TDD -- not because I knew they were important, but because that was
basically all I had to go on -- and lucked into a _mindset_ that
continues to serve me pretty fucking well. And I was motivated to learn
TDD _from scratch_, because without doing that I wasn't going to get a
job.

On the other hand, all but noise of the devs I know who write unit tests
for their code started doing it because they were _told to_. They had
jobs, they had a nice comfortable routine, and word came down from upon
high that "we're writing tests now, y'all!" So they had a browse of the
internet, maybe read a book or two, and decided that maybe unit testing
was a pretty good idea. Arrange-act-assert, run a thing through
Testdriven.Net, maybe this code is hard to test in isolation so let's
figure out how to mock out its dependencies.

It's easy, if you have a nice productive _routine_ figured out, to shove
the square peg of TDD into the, well, slightly _rhomboid_ hole of your
present practice with a couple whacks from a rubber mallet. And it's a
win! Now you have tests for whatever you implemented... and remembered
to test... and were able to test reasonably well. That's better than the
no-tests world you lived in before, but maybe not better _enough_ to
justify all the time you feel like you're spending going back and
writing tests for all the features that _just obviously work_.

## Pair programming

I told you that, so I could tell you this.

In my experience, self-described hard-nosed pragmatic get-things-done
programmers shit on pair programming about two to four orders of
magnitude _more_ than they do on test-first TDD.  "It's a waste of
time!" "It's like a glorified screencast, except I can't fast-forward
through the boring parts!" "Pairing with someone who doesn't think about
code the way I do sounds like a living hell!"

Friends, as of this writing, I don't like pair programming. At best I
flash back to when I was TAing intro programming courses, watching
someone walk me through the code they just wrote and silently tabulating
the difficulties I can see coming. At worst, it's an awkward,
half-declared dick size war of methodology and ideology.

And that's because I _suck_ at it.

See, nobody told me I'd have to become expert in _all_ of eXP's
practices before I got hired at that particular job. I never had to
actually _learn about_ pair programming before my team lead said "Hey,
you could pair with that guy and learn a bit about this domain". I just
sort of figured that pair programming was _one of those things_ you
could just _pick up_ as a developer, maybe a bit harder than figuring
out why ORMs are cancerous but a bit easier than grokking monoids.

Nope!

What I'm learning -- painfully, the hard way -- is that pairing is a
very specific skillset that takes _effort_ to learn, on both sides of
the fence. All of the luminaries of the XP movement did their level best
to save me this pain and struggle, if only I'd listened to them, but I
didn't really get exposed to pair programming _qua_ pair programming
until maybe two weeks ago.

It's a _practice_, and just like red-green-refactor you need to learn
the _practice_. There aren't any sexy tech docs to retreat into for pair
programming like there are for testing ("Oh hey, guys, we can work
consumer contracts into our continuous integration framework!" has no
equivalent when two people sit down at one keyboard and look at each
other awkwardly).

And yet.

And yet I've never worked anywhere that tries to _teach_ devs how to
pair with each other. It's always an assumed skill: "Oh yeah, if you run
into trouble you can pair with Matt, he knows that codebase pretty
well." Yeah, but he doesn't know how to _pair_ because he's never
_learned_.

Imagine my surprise when, after three or four modestly to
brain-explodingly informative pair-programming sessions, I decided to
see if anyone had systematized _learning_ to pair. I came across a few
8th Light blog posts which just _casually assumed_ that the first thing
you'd do when sitting down to write code on someone else's ticket was,
like, _talk_ to them and try to understand what they were trying to do.

This has never, ever, _ever_ happened to me. I sit down and the other
dev just starts walking me through the code at a micro level, and until
today I've just stupidly accepted that _that's just the way it is, man!_

Pair programming takes _effort_, and it takes some basic level of
_skill_, from _both_ sides of the pair. Every time I read an 8th Light
article about pairing, it starts with the pair having a quick chat about
what exactly they plan to do. Sounds obvious, right? _I've never done
that._ Nobody's ever stopped me and said "Hey, let's talk about what
we're pairing on". This is everybody's fault, but it's not _negligent_
-- it's merely _ignorant_.  Nobody _told_ us pairing would take this
much attention to detail!

Well, except Kent Beck. And Uncle Bob. And everyone else, if only we'd
thought to read their books and blogs and so on for _comprehension_.
