---
title: "The Three Ways of DevOps"
date: 2020-02-25T07:48:54Z
draft: true
series:
  - The Three Ways of DevOps
tags:
 - devops
 - podcast
toc: true
summary: |
  Learn the "Three Ways" of DevOps: flow, feedback, and learning as
  measured by lead time, deployment frequency, MTTR, and change
  failure rate.
---

I've written and spoken about DevOps extensively. In fact, I
devoted the first episode of [Small Batches](https://smallbatches.fm)
to the topic. What follows is a short and sweet introduction to the
high level ideas. Here's the same content in text or audio.

## The Three Ways of DevOps

{{< transistor "https://share.transistor.fm/s/c72e76bc" >}}

This is it, the first episode of my podcast! The new year gave me the
push I needed to start shipping.

I launched this podcast to share ideas and practices that have helped
me throughout my career. I write each episode to be short and
informative so you can fit them in over a cup of coffee (or sometimes
two). Think of Small Batches as a free form anthology on the wide
world of software engineering and business.

Let's set the stage before we dive into today's topic. My goal as a
software engineer is create systems that are easier to build, test,
deploy, and operate in production. I achieve those goals through
DevOps.

DevOps connects our work as engineers to business value. Exploring,
internalizing, and implementing DevOps changed my career. I've spent
the last few years reading and writing about DevOps, so there's no
better way to launch this podcast than introducing DevOps.

For this, I turn two of the best books on the topic: The DevOps
Handbook and Accelerate. Both are written by Gene Kim (you may also
know him from The Phoenix Project and now the Unicorn Project) and
other coauthors. The DevOps Handbooks introduces DevOps principles and
their associated technical practices. Accelerate provides metrics to
measure progress and evidence of DevOp's effectiveness. You need both
to understand DevOps.

The DevOps Handbook introduces the "Three Ways of DevOps". They are:
flow, feedback, and learning. Each build on the other to create a
feedback loop between technology and business. Accelerate defines four
metrics: lead time, deployment frequency, mean-time-to-resolve, and
change failure rate. Here's how two fit together.

### Flow

Flow, the first way of DevOps, establishes fast flow from development
to production. Organizations achieve this goal by breaking work into
smaller batches, preventing defects with continuous integration and
automating deployments. These practices fall under the Continuous
Delivery umbrella. Teams can measure their flow with two metrics: lead
time and deployment frequency.  Leads time is the time it takes to go
from commit to production. Deployment frequency is simply how often
deploys happen.

### Feedback

Feedback, the second way of DevOps, establishes right to left flow of
telemetry across the value stream to ensure early detection and
recovery or prevent subsequent regressions. The idea is to use
production learnings to drive subsequent developments. Here's some
examples: say you just shipped a new feature, how is engagement
measured? Another: Are their metrics or logs that engineers can use to
monitor system health? One more: do we know how long are builds are
taking? Teams can measure the second way with the well known
mean-time-to-resolve (or MTTR) metric.

### Learning

Learning, the third way of DevOps, enables a high-trust culture
focused around scientific experimentation and learning. The idea is
that once work is shipping out to production quickly and the telemetry
is in place to across the value stream, then teams should improve
their processes through scientific experimentation. The principal of
flow enables teams to quickly ship new business ideas or process
improvements. The principal of feedback ensures teams have the
information to empirically validate their ideas. Organizations apply
this principle through activities such as blameless postmortems and
A/B tests. Team can measure the third way by tracking their change
failure rate. That is the percentage of changes that result in
degraded service or require a follow up action like a patch or
rollback. Although I offer a different interpretation. I think of it
as the percentage of changes that did not deliver the expected
results--but that's a topic for a future episode.

I have much more to say on all these topics but I'll leave that for
future episodes. Let's recap: Apply continuous delivery for fast flow
from development to production; add telemetry across your process and
use it to drive future decisions, then strive to improve both those
processes. Measure your progress with lead time, deployment frequency,
MTTR, and change failure rate.

Your trajectory should be to decrease lead times, increase deployment
frequency, decrease MTTR, and decrease change failure rate. Or in
other words, as you improve velocity then stability comes along for
the ride.

Alright, that's wrap on this episode. Go to smallbatches.com for show
notes, a transcript, and links for my review and analysis on DevOps
Handbook and Accelerate. Also subscribe to this podcast to receive
future episodes.

Until the next one, good luck out there and happy shipping!
