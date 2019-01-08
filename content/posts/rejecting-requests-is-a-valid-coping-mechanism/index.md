---
title: "Rejecting requests is a valid coping mechanism"
date: 2019-01-08T17:03:56Z
draft: true
featured_image: "posts/rejecting-requests-is-a-valid-coping-mechanism/images/featured.jpg"
tags: []
categories: []
series: []
---

Intro section goes here (before the "read more" section). Shouldn't be more than about 70 words.

<!--more-->

One of the ways to handle an unexpected high load is to reject some requests. While it's understandable that doing so likely upsets the users being affected, the alternative is much worse. In scenarios where we don't put an upper bound on the number of requests, we may get into a situation in which the server spirals out of control trying to serve everything.

Servers have finite resources - the number of CPUs, size of memory, I/O and network speeds, to name a few. The application's performance and ability to utilise the multi-core environment also comes into play. These resources ultimately limit the amount of processing the server can do.

There is a correlation between response times and the number of in-flight requests.

When serving requests, the server spends its resources. Let's consider a situation where an 8-core server needs to process the uniform requests. Let's assume that when the server is idle, processing takes 200 ms.

The easy one is when up to 8 requests come in at the same time. Given 8 cores, each of them is processed parallelly, and as such, served in 200 ms. (Ignoring a couple of other factors here, such as OS scheduling and OS processes for the sake of simplicity).

If we double the number of requests to 16 and assume that they arrive the same millisecond, the situation becomes more complicated. Our gut may tell us that the requests are processed sequentially; do the first batch of 8 and then continue in batches until the requests are gone. Doing it this way would mean that the first batch takes 200 ms to complete, whereas the second batch takes 400 ms (200 ms waiting + 200 ms processing).

Process scheduling does not work this way, however. Instead, the Operating System continuously schedules the work for the processors. This constant scheduling means that at any given point, the OS may instruct the CPU to stop its work, save the state, switch to another task, load the state, and continue. This procedure is called "context switching", and has a minute cost to it.

The effect is that, on average, the requests complete in approximately 300 ms ((8*200 + 8*400) / 16 = 300 ms)

As an analogy, think of filling up an [ice cube tray](https://en.wikipedia.org/wiki/Ice_cube#Ice_cube_tray). Instead of filling up the individual cube moulds one after the other, you move the tray around, filling up each mould to some extent, stopping when all of them are sufficiently filled. This way, each mould takes more time to be filled; however, none of them has to wait for too long to be done.




1. A request comes in that needs 200 units of resources. The server takes 20 ms to serve the request (20 * 10 = 200).
2. 10 requests come in that need on average 350 units of resources. The server takes, on average, 35 ms to serve each of the requests. However, since the server is only able to work on 8 things at the same time, it will 





The more resources a request requires, the longer it takes to fulfil it. Conversely, 


There is a correlation between response times and the number of in-flight requests.

If we accept that the resources in a server are not infinite, then we should also consider that there is a correlation between response times and the number of in-flight requests.



## Cascading failure

According to [Wikipedia](https://en.wikipedia.org/wiki/Cascading_failure):

> A cascading failure is a process in a system of interconnected parts in which the failure of one or few parts can trigger the failure of other parts and so on. (...) Cascading failures may occur when one part of the system fails. When this happens, other parts must then compensate for the failed component. This, in turn, overloads these nodes, causing them to fail as well, prompting additional nodes to fail one after another.


<!-- Credit to the bottom -->
<sub>Featured image credit to [qimono on pixabay.com](https://pixabay.com/en/sunrise-space-outer-space-globe-1756274/)</sub>
