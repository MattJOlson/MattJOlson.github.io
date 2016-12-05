---
layout: post
title: In Defence Of New Toys
---

I found a pretty good twitter thread earlier today, in which @drboolean
[kicks off matters
thus](https://twitter.com/drboolean/status/805152967024209920):

> You shouldn't program w/ X because not everyone knows X is a common
> arg I hear. That leaves us w/ beginner primitives & a popularity
> contest

I took the opportunity to snark about 1990s-era C++, but @theskaterdev
[put me on an excellent train of
thought](https://twitter.com/theskaterdev/status/805445617002643462):

> especially considering the increased cost of hiring and potential
> impact that has on speed of development.

[Then,
later](https://twitter.com/theskaterdev/status/805515374703837185):

> us devs love to learn new things though and use that learnt skill like
> it's the only way of doing things :)

That there is what I've seen as New Toy Syndrome, and I think it's
undervalued in the corporate, enterprise-y dev environment. Yes, that
means I think we should have more of it. Lemme 'splain.

## The Professional Developer

Let's start with this: As a professional software developer, my job
isn't writing software, it's _delivering value to the business_ by
writing software. That's obvious, right? I'm not going to go to work
tomorrow and hack on a raytracer, although it'd be fun and I'd do a good
job. I'm going to go to work tomorrow and hack on problems that're
going to make, or save, the business money.

So what's the point?

_Decisions around new tech, at work, need to be grounded in business
value._ That's the "professional" part. But that actually says _less
than you think_ about whether you should try out that neat new SPA
framework, or rewrite the back-end in Haskell, rather than struggling
along in whatever ancient, established framework has ossified the
codebase and slowly grown you an ulcer.

### Misapplied Grit

And yet, I keep seeing otherwise bright-eyed, clever, enthusiastic devs
labouring desperately to _push aside_ the Cool New Tech that might make
their jobs easier (and more fun!) in order to signal that they're _too
professional_ to come down with New Toy Syndrome. "Yeah, I like playing
around with Elm on my own time, but I'm on the company dime right now
and we're sticking with Angular 1.x because that's our agreed-upon
technology-choice best practice."

Yeah, no.  There are plenty of good reasons why you might want to stick
with the _status quo_ -- maybe you're working to a fixed deadline and
don't have space for the risk of new tech.  Grinding along on a
suboptimal _status quo_ because you're afraid to look like a special
snowflake isn't "being a professional", it's ducking the problem.

### A False Dilemma

"When you've just learned category theory, everything looks like
Kleisli composition." The big lie behind New Toy Syndrome is that it's
an either/or, all-or-nothing proposition... and that the "all" side is
necessarily risky and irresponsible.

Guess what? It ain't.

New tools are just that, new _tools_. Think of them the way your product
manager thinks about stuff developers get excited about: What's the
risk, and what's the reward? If your PM's currently worried sick about
extra schedule risks, find ways to introduce your new shiny with
built-in risk mitigation -- timeboxed experiments, say, or ["oh, it's
just test
code"](https://fsharpforfunandprofit.com/posts/low-risk-ways-to-use-fsharp-at-work-3/).
If you're in a spot to drive your process forward, find ways _you and_
your new toy can do that -- lunch-and-learns, pilot projects, emphasize
and measure the expected benefits.

While you're at it, measure (and weigh) the cost of failure. What if you
get into that greenfield ClojureScript project and find out that it's
utterly incompatible with your deploy pipeline? Identify the risks,
acknowledge them, and find ways to mitigate them -- and suddenly you can
talk about them in a cost/benefit context rather than as scary stories
that product managers tell the interns over a campfire.

### Back To Professionalism

If you want to bring your new toy into your corporate mainstream, you're
more or less obliged to do it in terms of business value. Why do you
like F# so much -- fewer bugs and less boilerplate? Quantify that. Sell
it.

See what you're doing? You're _giving your company a chance to grow, to
get better._

Maybe you're worried about using your new favourite API for _all the
things._ Maybe your team lead's worried about you doing that. Maybe it's
not such a terrible idea! If nothing else, it'll give you a bunch of
data (or at least reasonably informative anecdote) about where that API
works well and where it just doesn't fit. Those stories have value. (Are
they worth the time and effort? Well, what would you have done instead?)

Holding good ideas back because you're worried about looking like "that
guy" is unprofessional.

## A Few Cultural Benefits of New Toys

I started writing a list of all the technical things you miss when you
refuse to try new things, but it's largely stuff you already know if you
give even half a shit about this topic. However, when you introduce your
favourite new toy to the company, you're not just improving your tech
stack.

### Hiring And Retention

People worry that, if we rewrite our J2EE backend in Erlang, we're going
to have a hard time hiring people to maintain and develop it. Then they
complain that, when they ask their recruiters for enterprise Java
developers, they get a thundering herd of staggeringly mediocre
candidates.

I submit that your company would probably find more high-end candidates
-- and at a _discount_ -- by hiring people who don't _have_ those
outlier skills but _want_ them. You want people who are motivated to
learn and improve, right? Why not accept that as part of the job
description?

The same logic applies to current developers.

For my money, the biggest positive effect this has isn't making
individual devs happy and engaged -- it's building a culture where
those devs can bring their opinions on The Next Big Thing to the
business, and have those opinions respected and acted upon. That's devs
being engaged and wanting to make things better, and managers trusting
those devs to be invested in the business -- not just punching keys in
exchange for a paycheque. 

### Flexibility

When I started an F# pilot project in my very C#-dominated company, I
spent far more time wrestling with tooling than I did writing code. I
wanted to make the CI and deploy stories for my Suave service as close
to the status quo as possible. I didn't want to leave behind a
special-snowflake build/deploy pipeline that nobody else really
understood.

This had the happy side effect of teaching me a lot more about how our
build-promotion-deploy process is set up, and _why_ it's set up that
way. And when I had to ask for changes ("what user should run Windows
services on this IIS pool?"), we weren't butting heads; we were working
towards the same goal more or less by default.

We found the parts of the process that were ossifying just by
coincidence ("Oh, nobody's tried this before except on IIS, but sure,
Suave works too"), and made them more flexible. That's opened up room
for other people to come along and do similar, though not identical,
things. A handful of better solutions to corner-case problems suddenly
came to mind.

Uncle Bob says, "If you want your software to be flexible, you have to
flex it." Process is the same way. Introducing new toys that flex -- but
don't tear apart -- the current process makes it more adaptable, and
(more importantly) gets people into the _mindset_ that process should be
made to serve them, not the other way around.

### Experimentation

Let's posit that, as a dev, you're bringing your favourite new toy to
work with the idea that it's going to bring business value. There's
always the question of "well, did it work?" How can you tell? Probably
you should make a prediction about the future, maybe in terms of some
measurable metric. Even if you can't do that, you're sort of obliged to
write up some lessons-learned and reflect on future improvements.

I've never seen anyone do that with "industry standard" technology. "Hey
guys, how's this integration database working out for us? Are we getting
value out of the ORM it's making us use?" Terrible things are just
accepted as the cost of doing business.

Once you start bringing in new toys, and evaluating them, that old
monolithic best-practices stack doesn't seem so inevitable any more. And
if you're lucky, you start to realize that you can bring in a new toy,
and watch it fail abysmally, and _still_ get value out of that failure
because now you have a better idea of your requirements. _That's_ the
win -- increased self-awareness, and increased willingness to improve.

## It All Comes Back To Trust

Unsurprisingly, devs generally want to have a good reason to take a risk
on behalf of the business and try something new that might fall flat on
its face. Equally unsurprisingly, managers and stakeholders want to have
confidence that the weird new gobbledygook that dev brought back from
their latest conference is likely to provide some balance-sheet benefit.

That's a matter of trust.

If the geeks and the suits at your company don't trust each other not to
screw the other party over, all of this is irrelevant. But if you _do_
have a sufficient level of trust -- and willingness to collaborate --
exercising it by bringing in your new toys is a great way to make it
stronger.
