---
title: "2018 in review"
date: 2018-12-21T21:59:38+01:00
draft: false
tags: ["review", "retrospective"]
---

2018 came and went pretty fast. While technically still in December, I thought I'd write up a summary for the past year, and with it, kickstart this site of mine.

<!--more-->

![2018 calendar](images/2018-header.jpg)
<sub>Image credit to [ulleo on pixabay.com](https://pixabay.com/en/calendar-2018-year-turn-of-the-year-2763496/)</sub>

Understandably, it's rather hard, as I don't have any place to look back to see what I've planned for the year. The truth is, I haven't had anything, I was just going with the flow, if you will.

### Good things come to those who think

One of the best things that came out of 2018, is me realizing that I didn't have any plans for the year. No clear-cut path to improve in, no fixed interests, no real idea of what I _really_ wanted to do.

Have you ever had the feeling that you don't really enjoy what you're doing or working on? And that you're pretty sure that you should change, but not sure what exactly? Or - have you had colleagues or employees who kept on complaining about their responsibilities, but when asked what they wanted to do about it, how they wanted to change it, they simply said "I don't know"?

![questions](images/question.jpg)
<sub>Image credit to [Anemone123 on pixabay.com](https://pixabay.com/en/question-question-mark-survey-2736480/)</sub>

I was like that, until about the middle of the year when I figured out what I really wanted to do. At 31 years. Better late than never I guess.

Mind you, I already knew it had something to do with computers and programming, but _what exactly that was_, I had no idea.

So I sat down and started to think about it, spent a couple of nights, and even weeks. The breakthrough came when I asked myself the following question:

> If I had to work during the weekend, what would I be working on?

And then it hit me. _I was already doing that_. There ~~were~~ are weekends (and weeknights) when I sit at my computer and just type away. The common aspects among them?

### Simplify and automate

In other words, creating tools to help others.

The biggest hobby project I had this year was a tool that parsed a Java project and built up a dependency graph based on what each of the classes were importing. This was in preparation of seeing whether there are any import cycles in there, and if so, how many.

> There were many import cycles. Surprisingly, I couldn't find any other Java projects in my brief search that _didn't_ have them.

Other than that, I kept ingesting knowledge.

### Docker and Kubernetes

![container ship](images/container.jpg)
<sub>Obligatory image about containers. Also, credit to [Julius_Silver on pixabay.com](https://pixabay.com/en/hamburg-port-of-hamburg-3021820/)</sub>

This year I went all-in on Docker, and moderately immersed myself in Kubernetes.

Docker appeals to me on a fundamental level - abstracting the execution of the environment from the actual environment in a small, easily sharable package is brilliant. Adding to that the mentality of statelessness (i.e. extra data needed by your app to operate) opened a lot of opportunities.

It also lead me to the world of container orchestration systems like Swarm, and eventually Kubernetes, which can take a bunch of containers and keep them alive. If they die, restart them. If the server dies, schedule them onto other nodes. Of course I'm over-simplifying what Swarm and Kubernetes can do, but this is the primary benefit that I saw in the beginning.

If we combine the statelessness of the containers with what Kubernetes (and, of course, Swarm) can do to keep them alive, we can remove humans from the operations side to allow them to work on more meaningful things, instead of just toiling away on keeping services alive.

Naturally, meeting these technologies and their ecosystem showed me exactly how much  I still don't know. Coincidentally, that was the third big focus in 2018:

### Improving, improving, improving

![bookshelf](images/books.jpg)
<sub>Image credit to [Free-Photos on pixabay.com](https://pixabay.com/en/books-bookshelf-library-literature-1245744/)</sub>

I have watched countless conference talks, read even more articles, did some online courses and had my fair share of books about programming (and DevOps).

If I had to emphasize the areas in which I've learned the most, I'd say they are microservices, programming practices, patterns and general mentality, Go (the language) and containers and container orchestration.

All of these topics have encouraged me to learn even more about them, as well as to try them out, wherever possible.

## Conclusion

That was the gist of 2018. Me figuring out what I wanted to do, meeting amazing technologies and ways of thinking, and adopting as much as I can.

Here's hoping 2019 will be even better!