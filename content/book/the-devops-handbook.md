---
title: The DevOps Handbook
subtitle: "How to Create World-Class Agility, Reliability, & Security in Technology Organizations"
link: https://itrevolution.com/book/the-devops-handbook/
cover: /images/the-devops-handbook.jpg
date: 2016-10-06
publishDate: 2018-04-23
author:
  - Gene Kim
  - Jez Humble
  - John Willis
  - Patrick Debois
toc: true
tags:
  - devops
  - value streams
  - theory
  - leadership
  - management
summary: |
  Increase profitability, elevate work culture, and exceed
  productivity goals through DevOps practices with this non-fiction
  follow-up to the bestselling The Phoenix Project.
---

## Background

Here's the book's pitch:

> Increase profitability, elevate work culture, and exceed
> productivity goals through DevOps practices. More than ever, the
> effective management of technology is critical for business
> competitiveness. This non-fiction follow-up to The Phoenix Project
> shows leaders how to replicate these incredible outcomes, by
> demonstrating how to integrate Product Management, Development, QA,
> IT Operations, and Information Security to elevate your company and
> win in the marketplace.

[The Phoenix
Project]({{< ref "book/the-pheonix-project" >}}) is a
fictional story about a struggling company and their transformative
success. The DevOps Handbook is manual for putting the changes in The
Phoenix Project into practice. The author's make strong claims about
increasing probability and success in the marketplace. Naturally all
business desire those outcomes. The books is light on the data side,
but rich with personal experiences, case studies, and anecdotes.

The author's split DevOp's practices into three ways:

1. The Principle of Flow: fast flow from left (idea/code) to
   production (right)
2. The Principle of Feedback: fast information flow right (production)
   to left (code)
3. The Principle of Continuous Improvement: building organizational
   feedback loops to keep things moving

DevOps encompasses far more than simply breaking down the barrier
between development and operations. It's a philosophy built on
feedback loops. Each of the three ways is a feedback loop in its own
way. First, lower lead times with continuous delivery so ideas make it
to production faster. Second; improve telemetry throughout the process
so failures are more quickly recognized and resolved. Third: build
organizations that leverage these feedback loops and empower everyone
to improve in their daily work. Four: (yes) profit.

The book is divided into three parts, one per way. Each part documents
the relevant technical practices with supporting case studies and
experiences sourced from industry professionals. It's no surprise that
companies like Netflix, Amazon, and Etsy are referenced often.

The author's note that three ways are not a linear progression. Every
team may have bits and pieces of each. This is where the DevOps
handbook shines. It draws a roadmap across them all so improvement
focused teams may fill their gaps.

## Thoughts

The DevOps Handbook is fantastic. I poured across the pages and found
many noteworthy passages. There is a ton of valuable knowledge and
insight in the book. Reading it put my feelings around DevOps into
words backed by statistics and practical implementation patterns.

It's no secret that I think that continuous deployment is the best way
to ship software. The author's focus on continuous delivery, but
there's enough overlap between them and the other practices they bring
along for the ride. I couldn't help but nod along through part one
until the continuous integration chapter.

Continuous integration, like many terms in software development, means
many different things to many different people. CI, to me, means
running automated tests against all commits to source control. My
definition is orthogonal to anything besides automating testing. My
definition of CI refers to practice of automated testing in the DevOps
Handbook. The DevOps Handbook defines continuous integration as the
combination of trunk-based development and automated testing.

Roughly speaking, trunk-based development requires developers to check
in code multiple times a day to trunk (or "mainline", or "master").
This gives me pause. My immediate thought was there's no way to do
away with topic branches. I remember the branching strategy rules in
my past teams and those published in blog posts. You may be familiar
with "git flow" with it's release, hotfix, and jumble of other purpose
built branches. This approach trips many people up because branching
strategy is interwoven with how they physically do their job. It seems
this a common reaction because the author's devote a small section to
addressing these concerns immediately after introducing the concept.

They acknowledge trunk-based development is the most controversial
practice they advocate for. I imagine the controversy stems from the
fact that trunk-based development drastically changes how people do
their work. TDD, and CD faced the same resistance when they were
introduced. CI may be the last domino. The authors do their best to
dispel the controversy with experience and case studies. Their
position is that branches are useful. Long running and complex
branches are not because they have a negative impact on productivity.
Trunk-based development mitigates the riskby reducing batch sizes
(since smaller branches are easier to write, test, and integrate).

The CI chapter made me revaluate some past decisions and their local
and wider organizational effects. I'll take trunk-based development
more seriously from this point on.

Two terms from the DevOps Handbook resonate with me: lead time and
batch size. It's no surprise that "lead time" and "batch size" are
peppered across this review. Lead time is the time to go from customer
request to code running in production. Batch size is roughly
equivalent to the size of a particular change. Of course the two are
connected. Smaller batches (such as 20 line method change) are easier
to develop, test, and deploy. This reduces lead times building an
important feedback loop. You'll find these terms mentioned throughout
the text. Both are helpful in framing your (or anyone else's)
organization's problems.

The problems facing you (or your organization) are likely technical
and organizational. The authors hammer home the point that DevOps is
not simply technical practices. It's the sum of organizational
practices and technical implementations. There's plenty of focus on
the organizational side throughout the text. I didn't expect to read
about Target here, let alone be impressed by their DevOps dojo. That
just goes to show that any organization can do DevOps and do it well.

## Highlights & Take-aways

Admittedly I have a hundred or so notes and highlights. Here are the
ones that resonated with me the most.

> In DevOps, we typically define our technology value stream as the
> process required to convert a business hypothesis into a
> technology-enabled service that delivers value to the customer.

This passage made me change how I wrote and talked about DevOps.
"Business hypothesis" sounds a lot like lean. Lean and DevOps dovetail
into each other nicely.

> In addition to lead times and process times, the third key metric in
> the technology value stream is percent complete and accurate (% C/
> A). This metric reflects the quality of the output of each step in
> our value stream.

I had not encountered this metric until the DevOps Handbook. I
realized that precent complete/accurate would have helped quantify
problems in my previous organization.

> Internally, we described our goal as creating "buoys, not
> boundaries." Instead of drawing hard boundaries that everyone has to
> stay within, we put buoys that indicate deep areas of the channel
> where you're safe and supported. You can go past the buoys as long
> as you follow the organizational principles. After all, how are we
> ever going to see the next innovation that helps us win if we're not
> exploring and testing at the edges?

This is my favorite passage from the book. I used to be a lifeguard so
the analogy really resonated with me. Teams need structure to succeed
in common work and the freedom to break the mold when the situation
calls for it. More importantly you have to trust the team to wade past
the buoys and handle the risks accordingly.

> The implications of the Kohavi data are staggering. If we are not
> performing user research, the odds are that two-thirds of the
> features we are building deliver zero or negative value to our
> organization, even as they make our codebase ever more complex, thus
> increasing our maintenance costs over time and making our software
> more difficult to change. Furthermore, the effort to build these
> features is often made at the expense of delivering features that
> would deliver value (i.e., opportunity cost).

There's the stark truth for many product organizations where plan
according to gut feel. My take-away: don't guess; know. Repeated poor
guesses reduce moral and eventually lead to burnout — or worse.

> As Mike Rother wrote in Toyota Kata, "As tempting as it seems, one
> cannot reorganize your way to continuous improvement and
> adaptiveness. What is decisive is not the form of the organization,
> but how people act and react. The roots of Toyota's success lie not
> in its organizational structures, but in developing capability and
> habits in its people. It surprises many people, in fact, to find
> that Toyota is largely organized in a traditional,
> functional-department style."

This passage hammers the point that people's habits and practices are
far more important to long term success than organizational structure.

## Recommendation

I don't have a bad word to say about the DevOps Handbook. It's a
practical roadmap to improving IT in any organization. It's also the
most valuable book on software development I've read in the past 10
years. I think anyone curious about DevOps or improving their
organization should read this book. I'd be shocked if you didn't find
anything valuable.
