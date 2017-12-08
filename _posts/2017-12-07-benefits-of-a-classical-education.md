---
layout: post
title: So, <em>should</em> you do a CS degree?
---

I was *planning* to get back into blogging either with a nice crunchy
"metrics in F# with Suave and Logary" post or a book review of Camille
Fournier's [The Manager's
Path](https://smile.amazon.com/Managers-Path-Leaders-Navigating-Growth/dp/1491973897/ref=sr_1_1?ie=UTF8&qid=1512694475&sr=8-1&keywords=the+manager%27s+path)
(tl;dr: Yes, you should buy it and read it), but apparently we're doing
the key fundamentals vs. credentialist signaling thing on the Twitters
lately so here's what finally bubbled to the top.

# tl;dr me, should I do a CS degree?

That's a hard _maybe_.

# Back up, buckaroo; what makes you an expert?

To start with, I have a Ph.D. in computing science. I spent about a
dozen years in school. My parents also have Ph.D.s, so I'm maybe a bit
more steeped in academic culture than most industry developers.

Oh yeah, I'm also an industry developer. Not just that, I've been
managing and _hiring_ industry developers for the last year or so. I
have a great dev on my team with a Master's degree in CS, and another
great dev with a certificate from a tech college. They both perform at
about the same level ("high").

I also, uh, _know of_ some people with CS degrees who stopped learning
as soon as they could manage and consequently don't add a hell of a lot
of value.

# So, what's so great about doing a CS degree?

Well, from my own experience, I got exposed to a lot of theory. I don't
_draw_ on it much, except to occasionally tell people they shouldn't use
regexes for that thing, but it built a strong foundation in my mind that
programming _can_ and _does_ have a basis in theory. It's not just an
ad-hoc, learn-the-SOLID-principles then debug until the tests go green
exercise; there are deep foundational truths you can use to build better
software.

I also got exposed to a fair amount of math. Again, I don't draw on it
much (which is a shame, I _like_ linear algebra and graph theory), but
again it gave me some basic tools to learn the math I _do_ use on the
fly. (Which, if you're wondering, is mostly set, ring, and group
algebra. I snuck in a _bit_ of products-and-coproducts category theory
today, but didn't call it that.)

# But what about coding?

Oh yeah, I wrote a _bunch_ of code, especially in grad school. I'm not
sure how much it helped, though; outside of my intro Software
Engineering course nobody really gave half a fuck whether my code was
any good as long as it shat out the results the TA was expecting.

Even so, spending a full semester in a team of four people building a
compiler was a pretty good exercise, and writing up honest-to-goodness
New Shit in grad school was exciting.

# So what's _not_ great about doing a CS degree?

Well, it's expensive. Between TAing and a 16-month internship I came out
of my B.Sc. pretty much even, but doing a Ph.D. is a fantastically
effective way to blow away probably seven figures of lifetime income. I
spent eight years earning $18k and came out the other side looking at,
if I was lucky, the top quartile of "junior developer". Things would be
even worse if I'd stayed in the "academic pipeline" of never-ending
postdocs and adjunct positions.

This is in Canada, mind you. I scraped by without student loans,
although I'm still not quite sure how I managed. Taking on debt,
especially for a grad degree, and expecting to convert that into future
earnings looks to me like a gamble with a massively negative expected
payoff.

# Okay, it's expensive. But you're a better developer, right?

Har.

When I was taught the fundamentals of software dev, I was taught that
code reuse was the holy grail and the best way to do it was inheriting
implementation code into subclasses. When I was taught databases, it was
assumed that any competent organization would have one single integrated
database managed by an aloof clique of demigods called DBAs.  When I was
taught networking, it was assumed that the code on the other end of the
socket would pick up.

When I got to grad school and started to build out a set of libraries to
support my research, I'd just picked up Kent Beck's [TDD By
Example](https://smile.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530/ref=sr_1_1?ie=UTF8&qid=1512696899&sr=8-1&keywords=tdd+by+example),
so I wanted to write myself a test suite. I was told it was a stupid
waste of time. (I did it anyway, at least to start with, but didn't
stick with it.) A year or two later, a labmate and I got interested in
pair programming... you can fill in the rest, right? We didn't stick
with it.

# But where _else_ are you going to learn crucial skills?

My team runs a couple of 24/7 back-end services. We deploy, I dunno,
half a dozen times a week. The people who do well are good at:

- Understanding why we're working on the tickets we're developing; even
  if they aren't talking to stakeholders there's some sense of a
  customer who wants this thing
- Test-driving their work
- Giving and receiving code reviews that're educational to both parties
- Building, running, and monitoring systems at scale that integrate with
  rather a lot of other systems

I have never run across a candidate who learned any of those skills in a
CS programme. Fortunately, there's a lot you can do to learn either on
your own, or (if you're working for a company that isn't terrible) on
the job. A CS degree might give you better _context_ for learning as you
go, but it won't substitute for learning as you go.

# So _should I_ do a CS degree?

I mean, if you want, it's certainly not going to hurt. It's probably
going to help. Aside from the "it's not _what_ you know, it's _who_ you
know" benefits of internship/co-op programmes and hanging out with a
bunch of people who're at least hypothetically motivated to build
systems, it'll give you plenty of practice at writing fairly nontrivial
code and learning difficult technical topics. Just don't expect it to
teach you all, or even most, of what you'll need to know.

It also gives you some opportunities to do things that'll serve you in
good stead down the road. Work as a teaching assistant for your
favourite professor; volunteer (I mean, ideally get paid, but colleges
gonna college) at the help desk; do programming contests; go out
drinking with grad students and pick their brains about the neat shit
they're into.

But if you can't afford a CS degree, either in time or in cash money
dollars, that lack shouldn't keep you out of the industry. You'll
probably have a harder time than you should getting in the front door --
credentialism is a favourite cop-out of lazy recruiters and hiring
managers -- but you're probably also bringing other skills to the table
that help you work as part of a team. And even if you're not, we learn a
lot on the job as we go.

Either way, probably don't do grad school.

# Appendix: Am I more hireable if I have a CS degree?

I can only speak for myself here, but... not _really._ Again, probably
there are a lot of HR turds and recruiters who substitute
pattern-matching on credentials for actually reading resumes for
comprehension, so in that sense, _yeah._ How much do you want to work
for those folks.

When I read a resume, or linkedin profile, or github repo, I look for
skill fit first. For me, for the jobs I've been hiring into, that's
basically this shit:

- Some reasonably modern back-end experience, ideally more than just a
  single language or stack
- TDD experience, or at least familiarity with unit testing
- Continuous integration and delivery
- Running a system at scale, particularly something horizontally-scaled
  and 24/7 available

After that, I look for things that make you stand out. Five years'
experience bartending? Hey, maybe you have social skills. Spent a few
years teaching grade school? Teaching ain't easy. Master's degree? I
have some idea of what that entails and brings to the table.

A four-year B.Sc. in computing science does not stand out, unless it's
from a really hot-shit school (in which case you're probably not
applying here). Lack of a four-year B.Sc. doesn't really stand out,
either.
