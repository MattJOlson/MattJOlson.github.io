---
layout: post
title: F# Advent Calendar - Testing Suave WebParts
---

One of the joys of working with [Suave](http://suave.io) is the
testability that falls out of its composition model. To make those tests
really sing, I've built a few helpers that wrap some of the underlying
type complexity. This in turn allows my tests to be more concise,
focused on the behaviour I'm building.

None of this is terribly complex, and that's part of the fun.

# A Brief Introduction to WebParts

Suave's routing logic is specified by composing WebParts, which are
functions on `HttpContexts`:

{% highlight fsharp %}
type WebPart = HttpContext -> Async<HttpContext option>
{% endhighlight %}

Briefly, a WebPart takes an `HttpContext` as input, does something with
it, and returns an `option` over `HttpContext` -- either `Just a`, where
`a` is whatever the WebPart was intended to do, or `None`, indicating
that the WebPart doesn't care about this particular input. All of this
is wrapped up in an Async workflow, which we don't need to worry about
just now.

What's important here is that `HttpContext` contains all the properties
we care about when testing our routing logic. We're going to build a
bunch of tools that operate on `HttpContext`s, specifically focused on
unit testing.

For a deeper look at Suave routing, [have a look at the
docs](https://suave.io/routing.html).

# The Very Basics - Requests and Responses

So let's start by building a request, throwing it at our router, and
verifying that we get a 200 OK out the other side. We'll fill in some
basic request parameters on `HttpContext.empty`:

{% highlight ocaml %}
let GetRequest u =
    let uri = new System.Uri("http://some.random.tld" + u)
    let rawQuery = uri.Query.TrimStart('?')
    let req = { HttpRequest.empty with url = uri ;
                ``method`` = HttpMethod.GET ;
                rawQuery = rawQuery }
    { HttpContext.empty with request = req }
{% endhighlight %}

This is perfectly usable as-is, but we can separate some concerns by
splitting the method and URI parts, and calling them separately:

{% highlight ocaml %}
let WithUri u hc =
    let uri = new System.Uri("http://some.random.tld" + u)
    let rawQuery = uri.Query.TrimStart('?')
    let req = { hc.request with url = uri ;
                rawQuery = rawQuery }
    { hc with request = req }

let AsGetRequest hc =
    let req = { hc.request with ``method`` = HttpMethod.GET }
    { hc with request = req }

let GetRequest u =
    HttpContext.empty
    |> WithUri u
    |> AsGetRequest
{% endhighlight %}

This shows off our general pattern for building test data: We're writing
combinators on `HttpContext`, adding info as we need to. Once we've done
that, we can throw it at a WebPart and see what we get:

{% highlight ocaml %}
[<Test>]
let ``resource/ with an integer parameter returns 200 OK`` () =
    GetRequest "/resource/1337" 
    |> mySexyRouter
    |> ...?
{% endhighlight %}

(I'm using NUnit, but that's more or less irrelevant.)

So we threw in an `HttpContext` with a well-populated request, and we'd
like to examine the result... but we need to unwrap it first. This part
isn't as much fun as building a set of combinators, but it's still
pretty straightforward:

{% highlight ocaml %}
let expectSome hc =
    match hc with
    | Some a -> a
    | None   -> failwith "Expected 'Some'"

let extractContext aohc =
    aohc |> Async.RunSynchronously |> expectSome

let extractStatus hc = hc.response.status

...

[<Test>]
let ``resource/ with an integer parameter returns 200 OK`` () =
    GetRequest "/resource/1337" 
    |> mySexyRouter
    |> extractContext
    |> extractStatus
    |> should equal HTTP_200
{% endhighlight %}

Not as much theoretical fun as chaining combinators, but it does the
job. Note that `failwith` in `expectSome` -- if we get a `None` out of
our router, that thrown exception will have NUnit fail our test.

Notice what we're _not_ doing: We're not firing up an OWIN or Nancy
instance, installing an ASP.NET site, configuring a DI container so it
knows how to build controllers, or any other overhead. All we're doing
is calling a function!

# Knowing Where to Look

Let's try something else. Maybe our GET resource is supposed to return a
JSON document with the resource ID in it, and we want to do a simple
string match to verify that. We'll need a way to get the response body,
but that's not quite as simple as it seems:

{% highlight ocaml %}
let contentAsString hc = 
    match hc.result.content with
    | Bytes b -> b |> System.Text.Encoding.Default.GetString
    | NullContent -> ""
    | SocketTask st -> "OMG a socket"

[<Test>]
let ``resource/ returns the integer ID of the requested resource`` () =
    GetRequest "/resource/1337"
    |> mySexyRouter
    |> extractContext
    |> contentAsString
    |> should haveSubstring ``"id": 1337``
{% endhighlight %}

Nothing particularly surprising there, except maybe the structure of
`hc.result.content`. A lot of the Suave testing story involves digging
into the types in `HttpContext` and figuring out what needs to be set
(or matched on), where. For that, you'll want to keep
[Http.fs](https://github.com/SuaveIO/suave/blob/master/src/Suave/Http.fs)
open in a browser tab (or maybe an IDE).

# A Word About Routers


