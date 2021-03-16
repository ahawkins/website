+++
author = "Adam Hawkins"
series = [ "The Three Ways of DevOps" ]
date = 2020-03-10T00:16:42Z
draft = false
summary = "A look into the Principle of Flow which calls for fast feedback cycles from development to production."
tags = ["devops", "podcast"]
title = "The Principle of Flow"
+++

## Podcast Episode

{{< transistor "https://share.transistor.fm/s/83f51319" >}}

The process used to write code and deploy it production is biggest
contributor to your team's velocity. You've probably been in the
situation where something is seriously broken in production and you
need deploy a fix right now. You may have even tried to circumvent the
existing process to deploy it out faster. Simply put, the faster your
team can write and deploy code to production the better. This is the
principal of flow or the "first way" of DevOps.

The DevOps Handbook provides a two step process for achieving fast
flow from development to production.

* Step 1: use trunk-based development and continuous integration
* Step 2: use continuous delivery

You've like heard these terms before. They're thrown around and often
used incorrectly. Continuous integration is a prime example. I'll do
my best to clarify the right and proper way to achieve fast flow from
development to production.

The goal at the end of each development cycle is produce
production-ready builds from master that been verified in a
production-like environment and validated with automated tests. That's
continuous delivery in a nutshell. Continuous deployment takes it one
step further by automatically pushing code to production but that's a
topic for another episode. For now let's start at with trunk-based
development.

I bet the mere mention of "trunk" makes some of you shudder. Some of
you may even be thinking: "trunk what is madman talking about SVN for?
We use git so what's the point?" Well the point is reducing cycle
times from development to production. Trunk-based development
optimizes for team productivity instead of individual productivity.

The trunk-based development boils down to keeping branches small and
maintaining an incremental straight line of development. Branches
should be merged to trunk (or master) at the end of the day. They must
be covered by automated tests so it's clear which commits are broken.
This is the origin of continuous integration (and they're a lot of
"continuous" things in DevOps). This practices ensures commits are
smaller, thus easier to write, test, and deploy to production hence
improving times from development to production.

I can hear some of you saying: "Adam-wait, what the hell are you
talking about? How does this make any sense? What am I supposed to do
with my feature branches? What about our epic branches that are open
for weeks?" The answers to that question lies in a perspective shift
regarding individual roles and what a team values, but I want to put
these questions another way.

Would you rather work in your topic branch for as long as possible or
would rather get your code out the door and into production? I choose
production and you should too. Anyways, I don't want to get into the
weeds on this topic because it's somewhat controversial so check the
show notes for more links on the topic. Let's move forward to
continuous delivery.

The idea here is connect commits from trunk/master to an automated
deployment pipeline that verifies builds are fit for production.
Naturally this requires varying levels of tests and automation. Now
don't get lost in the statements from the blogosphere that you need
Docker or microservices to do this. These proclamations miss the point
that technical practices like infrastructure as code and automated
testing are more important than specific technologies. There's no
prescriptive solution but I'll provide you an outline:

1. Deploy code to a staging environment
2. Run a smoke test against staging
3. Deploy code to production, Ideally using a blue/green or canary
   deploy
4. Run smoke tests against production
5. All good? You’re done. If not, rollback.

Expand out to more pre-production environments as necessary. You may
have a dedicated performance testing environments, a manual QA
environment, or whatever floats your boat. Honestly, it doesn't matter
how many environments you have as long as promotion and verification
is automated as much as possible. However, your number of environments
will grow over time as your deployment pipeline becomes more rigorous.

Alright, that's enough for this batch. The principal of flow covers
reducing cycle times from development to production. Trunk-based
development backed continuous integration and continuous delivery is
the best way to do that.

The book Accelerate provides two metrics to measure flow: lead time
and deployment frequency. Lead time is how long it takes go from
commit to production. Deployment frequency is simply how often deploys
happens. Accelerate also breaks down these metrics into tiers.

Top tier lead times are under an hour. This means a developer can
start working on, and deliver completed code to production in under an
hour. Mid their lead times range between a week and a month. How does
your team stack up?

Anyways, that’s a wrap on  episode. Head over to the podcasts’ website
smallbatches.dev for a transcript, show notes, and links to my review
and further analysis on both the DevOps Handbook and Accelerate.

Until the next one, good luck out there and happing shipping.
