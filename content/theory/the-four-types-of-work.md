+++
author = "Adam Hawkins"
date = 2020-06-16T17:27:40Z
draft = false
summary = "The four types of work--features, defects, debts, and risks--under pin the Flow Framework"
tags = ["Flow Framework", "podcast"]
title = "The Four Types of Work"
+++

## Podcast Episode

{{< transistor "https://share.transistor.fm/s/cc8506ef" >}}

Every team needs a taxonomy to categorize the work they do. Taxonomies
make it easier to reason abstractly about work and its role in the
business.

There are two types of work on the surface: features and non-features.
Features require no further explanation. Non-features is a bigger
group. Bugs, or defects, fall into this category. Defects and features
do not account for all the _other_ work software teams do though.

Features and defects are easy to grok because they correlate directly
with business value. Features attract customers. Defects are broken
features or quality regressions. Teams do more than developing
features and squashing bugs. Engineers spike on new problems.
Developers refactor code and pay down technical debt. There’s the
routine maintenance of library updates and security features. These
don’t fit squarely into features or bugs, so how are they classified?

These examples demonstrate the remaining two types: debts and risks.
Activities like refactoring or updating libraries are debts because
they improve the system. This work focus on the team’s ability to
sustainability deliver the other three types of work. Risks address
security, privacy, or compliance exposures.

The four types of work create a zero-sum model for choosing which
support business objectives. If a team devotes one hundred percent
capacity to features, then there is no capacity to fix bugs, pay down
tech debt, or derisk the business. A start-up with fixed runway may
choose to do this. Subsequently, they may devote more capacity to
debts and bugs once they clear the runway. On the other hand, a
business with strong regulatory requirements, like banking or health
care, may allocate the majority of their capacity to risks since
that's a core business priority.

The point is that a business' distribution of features, defects,
risks, and debts will vary over time as business goals change. The
four types of work enable different members of the organization to
understand the business value of each and relative prioritization
trade-offs.

Now, let's step back.

Consider the three ways of DevOps: flow, feedback, and learning.
DevOps applies the three ways to the engineering value stream.
Ultimately, one of these four types of work will land in an engineer's
backlog. That's where DevOps kicks in. If we think more abstractly
then we can break free of the engineering centric perspective.

The principle flow states that work should move from development to
production as quickly as possible. Then the principle of feedback says
that information about production should drive future development. The
four types of work correlates business telemetry. Features provide
value. Fixing bugs improve quality. Each of those makes customers
happy. Paying down debts keeps costs down.  Mitigating risks keeps
other factors stable. So, work—features, defects, debts, and
risks—flow left to right across the value stream resulting in changes
to value, quality, cost, and happiness.

This is underpinning of the [Flow
Framework](https://flowframework.org). Mik Kersten introduced the Flow
Framework in his book "[Project to
Product][]" published
ITRevolution press. That’s the same publisher behind The DevOps
Handbook, Accelerate, and The Phoenix Project to name a few.

Here’s the tip of the iceberg.

The Flow Framework applies the DevOps principles to the entire
business. The Flow Framework models the business as [networked value
stream](https://www.youtube.com/watch?time_continue=4&v=E5VP3ioSRU8&feature=emb_logo).
The value streams turns "Flow Items" represented by the four types of
work into business value. Business can track their value stream
network with [four metrics](https://www.tasktop.com/flow-metrics):

1. Flow Velocity measures how many items were completed over a period
   of time
2. Flow time measures how long it takes go form "work start" to "work
   complete" including wait times
3. Flow efficiency is ratio of active vs wait time
4. Flow load measures the number of items in progress on a current
   value stream

There’s more to Flow Framework than I can cover in a single episode of
this podcast. I think this is a good jumping off point for your own
research. I’ve already written a dedicated guide to Project to Product
which you can get for free. Visit
[smallbatches.fm/9](https://smallbatches.fm/9) for links to [my free
email course](https://productsoverprojects.com), an [infographic on
the flow
framework](https://flowframework.org/wp-content/uploads/2019/06/Flow-Framework-poster-A4.pdf)
(trust me it makes much more sense visually), and other great
material from Mik Kersten.

That’s all for this one folks. Thanks for listening and happy shipping.

[project to product]: {{< ref "book/project-to-product" >}}
