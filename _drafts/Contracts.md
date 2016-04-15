---
layout: post
title: Documenting Interface Contracts
---

So I have a bounded context, and you have a bounded context, and we want
to chat. Okay, how do we agree on how we're going to chat?

# 1. We don't

This kind of sucks though.

# 2. We publish classes

We publish something like a NuGet package full of the DTOs we serialize
before we send them over the wire in JSON or whatever, and you link
against it and use them to deserialize our messages before mapping them
onto your own thing.

Now you have two new problems:

* You have to keep up to date with my NuGet package ("Oh, you can't
  deserialize our events properly? What version are you building with?")
* You're tempted to either a) use our DTO types straight-up, or b) use
  something like AutoMapper to convert our DTOs into _your_ DTOs

And we have two new problems:

* We have to keep track of a DTO type at the interface layer
* If we fail to publish our package when we update our interface, we
  don't find out until _your_ code starts failing

None of this is insurmountable, but we can do better.

# 3. We publish documentation

There's a wiki page somewhere, or markdown on github, or whatever. It
describes the messages we send across the wire in JSON. Maybe it's even
up to date.

Now the only product we need to produce is a wiki page. We can write and
serialize DTOs if we want, or just build random heaps of JSON, as long
as they conform to the wiki page. You don't have to maintain a
dependency on whatever module we'd have published, and you don't have to
serialize to a data type that makes sense for _our_ domain -- you can
pull out, combine, ignore, fold, spindle, and mutilate the various bits
and bobs of our messages as you please right at the interface layer.

Neither one of us is likely to know that our updates have broken your
assumptions until your code starts failing, though.

# 4. You publish tests

So you write contract tests that demonstrate how you expect to call our
interface.
