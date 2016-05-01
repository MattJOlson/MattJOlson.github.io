---
layout: post
title: Push Info In Context
---

(This is my first tilt at the windmill of communicating complexity in
software development. I'm sure there will be more.)

## Branch names

A colleague introduced me to a great idea in git: You can _give a shit_
about feature branch names. (That loud _thunk_ you heard from the West
Coast a month and a half ago was me facepalming.)

At my company, we associate tickets with branches by prefixing each
branch with the ticket name. There are reasons for this, but basically
it's just part of the company's development _zeitgeist_.  So if you know
that a ticket called FOO-1337 is the 1337th ticket created by (or for)
the FooBar team, you'll recognize that `foo-1337` is the feature branch
associated with that ticket.

That's great and all, but it doesn't tell you what's _in the branch_ you
just merged into yours. It works fine in the short term, because you've
watched FOO-1337 crawl across the Kanban board in our stand-ups, but it
makes feature archaeology (let alone cross-team communication) a pain in
the ass.

My colleague's solution is to add that information to branch names. The
first time I was included on a code review for
`foo-1337-add-flame-to-blue-widgets`, I felt shame that I'd never even
_thought_ to do so.

> "Oh, but there's so much more typing!" [You shouldn't be afraid of a
> little typing practice.]({% post_url 2016-04-25-Learn-to-fucking-type
> %})

It's not like we'd never done tricks with branch names before; we'd just
written branch names for our _own_ benefit.  I've created plenty of
branches like:

```
foo-451-second-try
foo-556-merge-762
foo-556-merge-762-for-real-this-time
```

which were perfectly clear to _me_. Probably not to you.

But now if I'm asked to review your pull request for FOO-1337, which
merges `foo-1337-add-flame-to-blue-widgets` into `foo-qa`, I don't need
to pull up the ticket to remember (or discover) what you were working
on, and even if I _do_ I'm already primed to think in terms of widgets,
particularly blue ones on fire.

Crucially, nobody's been _inconvenienced_ by this extra information. My
colleague didn't have to expend much effort to come up with his branch
name. I didn't have to dig it out of a ticket or a wiki page; it was
_right there_, the _first place I looked_ when I saw that I'd been
invited to a code review. Nobody emailed the team or spammed a chatroom.
It's not a magical methodology, but it's an improvement at the margin.

## Commit messages

Like any decent tool, once you've used it you start to find other
applications. As with branch names, our commit messages follow a
pattern formed by one part tooling and three parts "we've just _done_ it
this way for a while": `^FOO-1138:.*$`

In practice, that means a lot of:

```
FOO-1138: Starting
FOO-1138: Added features
FOO-1138: Fixed a test
FOO-1138: Done
```

Real helpful, right? How about I write something like this instead:

```
FOO-1138: Carving out a path for cheese quality on red widgets
FOO-1138: Hacked in red-white marbled widget Emmentaler path
FOO-1138: Acceptance tests for Mornay sauce now fail correctly
FOO-1138: Handling Doritos flavour dust properly, ready for review
````

It's not _perfect_ documentation of what, why, and how I changed the
codebase in each commit, but it's better than nothing. Certainly it's
better than trying to figure out intent from a set of out-of-context
diffs when you're merging in the last three commits and have to resolve
conflicts.

> Incidentally, this is another good reason to "commit early, commit
> often".

## Code pre-review

But why stop there? When I commit my last changes and raise a pull
request, I could just sit back and wait for the accolades to roll in...
or I could run through my PR _myself_ and be the first person to comment
on each file.

This gives me the opportunity to revisit parts of my code changes that I
haven't seen in a little while, which usually sends _me_ back to my
local branch three or four times and generates another commit or two as
I fix my shit before anyone notices it's broken. It also lets me

* Explain _why_ I did that thing with a lambda instead of the
  obvious-seeming library call that doesn't _quite_ work
* Give the reader early warning of files that read best in a
  side-by-side (or unified) diff, or files whose only diffs are trivial
  renames or other automatic refactorings
* Point the reader to a wiki page where we've laid out the design we're
  hoping to achieve over the course of a few tickets
* Point the reader to _another_ wiki page where we've untangled the
  behaviour of this shit-pot legacy type we need to keep around for that
  one integration, which is why I've done these terrible things with
  bare `object`s
* Brag about the subtle, years-old bug I fixed by replacing this XML
  string with a `Maybe`-ish microtype

## Generalizing: It's all right where you have to look

The unifying factor for all of the above, and all the great other ways
you and I are going to go forth and improve our work, is that _nobody
has to go looking for this information_.

* If I want to know what your branch is for, it's _right in the branch
  name_, which is right in front of me.
* If I want to know what your commit did, _it's right in your commit
  message_, which is right in front of me.
* If I want to know why you pulled out an interface for this service
  class rather than just make it static, _it's right there in your
  pull-request comment_, which is right in front of me.

If I have to go look up an email thread, or a comment on a feature
ticket, or a wiki page, or diffs for a commit, chances are I'm not going
to do it unless it's really important. Chances are I'm going to _resent_
having to do it if it _turns out to be_ important and nobody called it
out as such. I don't want to have to _pull_ these answers out of you
when I realize I need them, and you don't want to be interrupted by me
trying to do that, either.

But while this is a push model, it's not a very intrusive one. You're
not fire-hosing an email thread with "HAY GUISE THIS IS WHAT I DID IN MY
LATEST COMMIT Y'ALL", and nobody's cracking a whip over you to maintain
an exhaustive wiki-doc of your design decisions. People who aren't
looking for your added little _lagniappes_ aren't going to be bothered
by them.

## Generalizing: This isn't "foo--; // add one to foo"

None of these artifacts is _persistent_. Yes, that silly Voltron joke in
your latest commit message might get stored by the git server until
`time_t` wraps around, but odds are it's going to be in the public eye
for no more than a day or two. Your dignity will probably survive.

A comment you leave on a _pull request_ is visible only to people
reading that PR, and again, it's only likely to be relevant for a day or
two. Anyone who has to up that merge might find it helpful, but it's not
going to influence anyone else's perception of the code when they merge
in your changes.

Basically, _these nuggets of information stay in a narrow context_,
where they're appropriate. Compare that to code comments like:

```
    foo--; // Add one to foo <abc Jan/1993>
```

Who's this `abc` character, and why was he trying to increment `foo` in
1993? That's shit that your version-control system should be remembering
_for_ you.

## Antipattern: Commit police considered harmful

Do I really have to point this out? Trying to _make_ people seed their
code reviews with comments or name their feature branches informatively
is doomed to fail. Every once in a while I'll commit a changeset where I
did nothing but clean up formatting in the files I'm about to change,
and it looks like this in the log:

```
FOO-2525: Cleanup
```

That's basically indistinguishable from an exasperated dev working
around some stupid "all commit messages must have a comment explaining
what work was done" edict.

Besides which, you're much better off with a team of devs who look at a
suggestion like "leave little breadcrumbs where you can" and think "wow,
that could be really helpful" than with a team of devs who respond with
"fuck you, that's not my job" and need to be thumbscrewed into
compliance.

## And while I'm at it

My company maintains a large corporate wiki, because of course we do.
Wiki doc combines the worst qualities of the push and pull models I
handwaved at above -- it's effortful to write, effortful to find, and
often effortful to read -- but this particular wiki has on its frontpage
a list of the dozen or so most recent page edits. Those edits are listed
with no more info than "who done it" and "what page did they do it to",
along with a link to a wiki diff.

When I'm between tasks, or just need a five minute break from pounding
my head against AutoMapper, I like to browse that stream of edits. If
nothing else, it gives me a hint as to what else is going on in the
company, and every once in a while I find something useful for whatever
problem I'm working on at the moment. If I'm implementing flames for
blue widgets and I see that the VP Product has changed the "Widget
Combustibility Roadmap" page, well, that catches my attention.

If we devs start adding little nuggets of information to _our own_ event
streams, we can start to leverage the same effect. It's a simple matter
for me to have a quick look at the commits my team members -- hell,
probably the whole company -- have made over the last half hour, or day,
or whatever. If those commits have informative messages attached to
helpful branch names, so much the better.

(I think it's helpful, if not strongly indicated, for developers to
maintain that level of situational awareness... but that's another blog
post.)
