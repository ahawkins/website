---
title: "The High Velocity Edge: Part 5"
author: "Adam Hawkins"
date: 2021-04-06T22:54:05-10:00
tags:
  - continuous improvement
  - toyota
  - devops
series:
  - The High Velocity Edge
summary: |
  How to fail fast using Sakichi Toyoda's jidoka concept.
---

Welcome to part five of a series on Steven Spear’s 2009 book [The High
Velocity Edge][book]. Today, I’ll continue discussing the first
capability: design and operate systems to reveal problems when they
occur.

The underlying philosophy comes from two people: Taiichi Ohno and
Sakichi Toyoda.

Taiichi Ohno designed systems based on pull based work called
"kanban". Kanban ensured work was only done in response to customer
requests, thus always serving the end customer and minimizing waste.

Taiichi Ohno eliminated waste by focusing on global outcomes. Sakichi
Toyoda eliminating waste by preventing defects.

Sakichi Toyoda started the family enterprise that would eventually
become Toyota. Sakichi’s work on an automated textile loom is relevant
to our story. Here’s Toyota’s take on the company lore:

> Women in his village, including his own mother and grandmother, wove
> fabric for clothing on hand-powered looms. Toyoda observed that they
> faced a heartbreaking scenario. If one of the hundreds of threads on
> the loom snapped, it created a defect in the material. Most of the
> time the weaver wouldn’t notice and continue weaving. The result was
> fabric better suited for rags than clothing.

> Toyoda committed himself to solving this problem. He invented a loom
> that would automatically stop at the moment a strand broke. This
> gave the weaver a chance to fix the problem before continuing their
> work. He built a machine that assured that all work is the work
> intended and doesn’t produce scrap. He dubbed this concept “Jidoka”.

[Jidoka][] is inseparable from the legendary Toyota Production system.
Sakichi’s idea was that work should be designed to identify problems
when and where they occur.

We call this "fail fast" in software. Identifying problems is
prerequisite to solving them. Toyota applied this idea at scale which
created high speed [kaizen][] (or continuous improvement).

I can explain jidoka through my own experience.

I just committed a change to application configuration related to
environment variables. I deployed the code to production. After the
some time, the deployment failed because of a missing environment
variable. This wasn’t the first time this happened to me. I had just
chocked it up to business as usual. Mistakes happen right?

Not this time. I thought: "wait. I can do something about this." My
code has latent assumptions about its runtime environment. How is this
different than my tests? My tests make explicit assumptions by
asserting on preconditions. If the preconditions fail, then the
outcome is a guaranteed failure. So the tests don’t run in that case.

How is this any different? Why should a potentially long running
deploy _even start_ if the preconditions aren’t met? It shouldn’t.

I, just like Sakichi, was tired of seeing waste created from
detectable defects.

So I set about writing predeploy checks for the target environment.
They verified things like: are all environment variables set? Does
the application start in a dry run mode? Can the application connect
to all configured database? Are API keys for external services valid?
These checks protected future changes from deploying into known bad
conditions. [Preflight checks][] were born. My thinking has never been the
same.

I’m constantly finding ways to apply jidoka to my daily work. That
practice demonstrated the value of `assert` statements _outside_
tests.

I didn’t use `assert` much in my code until recently. Now I use it
liberally. I’m always surprised by the problems they find.

I used to think that asserts only checked expected conditions. Asserts
should never fail, right? Wrong. They eventually will because
knowledge is imperfect. Reality will find ways expose the
imperfection. Then you’ll be thankful for the assert. That failing
assertion is telling you something is not understood. Go understand
it.

I challenge you to apply jidoka in your daily work. I guarantee it
will transform you thinking.

Now we have some philosophy in hand. I’ll go in the specifics of the
first capability in the next episode.

[book]: {{< ref "/book/the-high-velocity-edge" >}}
[preflight checks]: {{< ref "/theory/preflight-checks" >}}
[jidoka]: https://kanbanize.com/continuous-flow/jidoka
[kaizen]: https://en.wikipedia.org/wiki/Kaizen
