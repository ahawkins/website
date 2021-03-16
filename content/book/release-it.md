---
title: "Release It!"
subtitle: "Design and Deploy Production-Ready Software"
edition: 2nd
link: https://pragprog.com/book/mnee2/release-it-second-edition
cover: /images/release-it.jpg
date: 2018-01-01
publishDate: 2018-05-07
author:
  - Michael Nygaard
tags:
  - architecture
  - operations
  - SRE
summary: |
  A single dramatic software failure can cost a company millions of
  dollars — but can be avoided with simple changes to design and
  architecture. This new edition of the best-selling industry standard
  shows you how to create systems that run longer, with fewer
  failures, and recover better when bad things happen. New coverage
  includes DevOps, microservices, and cloud-native architecture.
  Stability antipatterns have grown to include systemic problems in
  large-scale systems. This is a must-have pragmatic guide to
  engineering for production systems. 
toc: true
---

[Michael Nygaard](https://twitter.com/mtnygard) wrote the first
edition in 2007. I read it a fews later and it drastically improved my
approach to software engineering. The book was especially helpful at
that point in time because I didn’t have real experience operating
production systems. It was a preview for what lay ahead and it
prepared me for it. Much as changed for me and the IT landscape over
the last decade. The second edition ports the lessons and perspectives
from the 1st edition to the modern landscape of cloud computing,
DevOps, continuous deployment, containers, microservices, and more.

## Background

> Software deliver its value in production. The development project,
> testing, integration, and planning…everything before production is a
> prelude. This book deals with life in production, from the initial
> release through ongoing growth and evolution of the system.

This quote from the introduction eloquently distills the approach
better than I can. Release It! is all about building software that
succeeds production. Production is a dangerous place. These days any
web service can see millions of users. Like it or not, Facebook has a
_billion_ users. Architecting systems and designing code to function
in these conditions is a challenge.

The book is a four part roadmap for improving production operations:

1. Create Stability
2. Design for Production
3. Deliver Your System
4. Solve Systemic Problems

Readers familiar with the first edition will recognize the case
studies. The airline grounded by an uncaught SQLException is painful
and still relevant.

I am happy to report that that 2nd edition moves away from a Java
heavy narrative to one one more grounded in cloud infrastructure, open
source, and DevOps practices. It’s no surprise that 1st edition took
this route. Things are vastly different now. There are three major
cloud providers now, DevOps is main stream, there are a plethora of
more languages in production (Node.js comes to mind), and containers
have taken infrastructure by storm. The second edition prepares you to
build production ready software with modern tools.

## Thoughts

Congratulations to Michael Nygaard on his writing! Nygaard comes
across as someone who has been through it all — from writing code in
the trenches, fighting outages, and architecting systems to survive it
all. He’s also been on the receiving end of outages that cost real
money — a fact that’s not lost throughout the text. His writing is
engaging, comical, and honest. This is refreshing in a technical book.

> Everything was on real hardware, no virtualization. Just melted
> sand, spinning rust, and the operating systems.

Nygaard always seemed to elicit a chuckle or jokingly date some
examples in the book. His telling of outage war rooms stories create
bonds with readers in similar situations. I bet that readers will
relate to carrying a laptop to family gatherings or going dark at
_exactly_ the wrong time. His advice doesn’t come from an ivory tower.
It comes from first hand experience.

Release It! recommends a philosophy for building production ready
software. Failure is inevitable, so it must be accounted for and
planned for. The goal is not to eliminate failure, but promote
durability and quick recovery times.

The book feels like an extension to the DevOps Handbook. The DevOps
Handbook provides three ways for building high performing IT teams:

1. The Principle of Flow (fast flow from development to production)
2. The Principle of Feedback (fast flow of production operational
   state to development)
3. The Principle of Continuous Improvement (continuing improving the
   previous two feedback loops by building organization and culture
   habits).

Release It! touches on all three ways. Part one (“Building Stability”)
relates to the principle of continuous improvement. Businesses cannot
move forward if production is constantly on fire. Part two (“Design
for Production”) relates to principle of feedback, or building
telemetry into production systems so informed decisions are possible.
Part three (“Deliver Your System”) relates to the principle of flow in
designing systems for continuous delivery/deployment. This is the crux
of principle of flow. Part 4 (“Solve Systemic Problems)” connects with
the principle of continuous improvements. Release It! advocates chaos
engineering as a means (and mindset) to routinely remove failure
points and increase reliability.

It’s no surprise that DevOps principles and practices surface in
Release It! I don’t think the author explicitly states that DevOps is
the best way to build, ship, and run software. However it certainly
feels like there’s a strong correlation if you’re familiar with the
topic.

The chapter on Chaos Engineering is welcome addition. I couldn’t
fathom this in the 1st edition. It’s another indicator how much the IT
landscape has changed and how we oriented ourselves in it.

Release It! contains a wealth of valuable information for teams and
individuals. This point sticks with me. Pay close attention to
integration points with any system. They will fail and take you down
with them if you’re not careful. Oh, and watch your thread pools and
queues!

## Highlights and Take-aways

> Every failing system starts with queue backing up somewhere

This quote refers to TCP listen queues. It’s simply good insight.
There are queues (likely they’re implementation details to your
abstraction layer) in front of everything. Things go hang wire when
they fill or overflow. ELB surge queue anyone?

> Design and architecture decisions are also financial decisions.
> These choices must be made with eye toward their implementation cost
> as well their downstream costs. The fusion of technical and
> financial viewpoints is one of the most important recurring themes
> in this book.

I appreciate that Nygaard drives this point throughout the book.
Outages cost real money. An [outage destroyed Knight
Capital](https://www.outagereports.net/in-the-matter-of-knight-capital-americas-llc-respondentpost-mortem/).
An outage may cost you $1,000,000 one day. The synergy between these
factors cannot be ignored.

> The main lesson is that not every problem can be solved at the level
> of abstraction where it manifests. Sometimes the causes reverberate
> up and down the layers. You need to know how to drill through at
> least two layers of abstraction to find the “reality” at the level
> in order to understand problems.

This quote comes from a scenario debugging application problems
originating in the networking layer. Systems sit on increasingly
higher abstraction levels, but they’re still exposed to failures in
lower levels. This is a good reason for reading and understanding code
at lower levels. In other words: if you use a framework such as React
or Rails, read the code and gain understanding.

> A new architect will focus on the boxes; an experienced one is more
> interested in the arrows

This quote is in parenthesis in the text, but I found it more valuable
than the sentence itself! Release It! is full of these quips. They
show me Nygaard depth of knowledge and experience. More importantly,
they point less experienced readers in the right direction.

> Hope is not a design method

This felt like a direct reference to the [SRE
book](https://landing.google.com/sre/book.html)’s “Hope is not a
strategy” mantra. This line of thinking makes Release It! a valuable
read for those in the SRE space.

> In time, even shockingly unlikely combinations of circumstances will
> eventually occur. If you ever catch yourself saying “The odds of
> that happening are astronomical,” or some similar utterance,
> consider this: a single small service might do ten million requests
> per day over three years, for a total of 10,950,000,000 changes for
> something to wrong. That’s more than _ten billion_ opportunities for
> bad things to happen. Astronomical observations indicate there are
> four hundred billion stars in the Milky Way galaxy. Astronomers
> consider a number “close enough” if it’s within a factor fo 10.
> Astronomically unlikely coincidences happen all the time.

Just putting a pin in that one then.

> Transparency arises from deliberate design and architecture. “Adding
> Transparency” late in development is about as effective as “adding
> quality”. Maybe it can be done, but only with greater effort and
> cost than if it’s been built in from the beginning.

Transparency here refers to production transparency provided by
telemetry systems. This is another common principle in DevOps
workflows: build production operational concerns in as soon as
possible. Things improve from there.

> The only real answer here is do your homework and commit to solving
> implementation challenges with whatever tool you choose.

This quote comes from a discussion on choosing a monitoring system. It
applies any big technology choice. There’s no silver bullet. At the
end of the day, you must know what you’re getting yourself into, then
learn to use the tools to get what you need done. Nothing will fulfill
100% of your needs out of the box, and even less likely, as things
change over time. Just choose, commit, and run with it.

## Recommendation

Release It! (Second Edition) is required reading for software
engineers looking to improve their next or current production system.
It’s especially useful to those wearing many hats. Personally, I think
less experienced engineers will gain more than experienced engineers.
This book is definitely for technical minded folks, so don’t bother
recommending it to your CEO or other upper management if you’re not
already having these conversations with them.
