---
title: "Building Evolutionary Architectures"
subtitle: Support Constant Change
edition: 1st
link: https://evolutionaryarchitecture.com
cover: /images/building-evolutionary-architectures.jpg
date: 2017-09-01
publishdate: 2018-05-02
author:
  - Neal Ford
  - Rebecca Parsons
  - Patrik Kua
summary: |
  The software development ecosystem is constantly changing, providing
  a constant stream of new tools, frameworks, techniques, and
  paradigms. Over the past few years, incremental developments in core
  engineering practices for software development have created the
  foundations for rethinking how architecture changes over time, along
  with ways to protect important architectural characteristics as it
  evolves. This practical guide ties those parts together with a new
  way to think about architecture and time.
tags:
  - architecture
toc: true
---

I picked up this book after hearing Neal Ford discussing software
architecture on [Software Engineering
Radio](http://www.se-radio.net/2017/04/se-radio-episode-287-success-skills-for-architects-with-neil-ford/).
He spoke eloquently and engagingly on architecture “(capab)-ilities”
and evolving systems. He elucidated many of my thoughts on the topic
and mentioned the book. A year later I made the time to read the book
and delve back into software architecture. This review covers
background information on the book, my thoughts, and a recommendation.
You should skip to the end if you’re purely interested in the
recommendation.

## Background

> We explore the ideas behind continual architecture: building
> architectures that have no end state and are designed to evolve with
> the ever-changing software development ecosystem, and including
> built-in protections around important architectural characteristics.

Building Evolutionary Architectures’ goal is to demonstrate the value
in building, and how to implement, evolvable systems that fit today’s
dynamic software landscape.

The process starts with identifying “-ilities” (their word for
characteristics such as “affordability” or “flexibility”), then
balancing the “-ilities” across dimensions such as technical
implementations or data storage, and verifying the “-ilities” in the
relevant dimensions with fitness functions. Think of fitness functions
as architecture tests. Now bundle the whole thing up as part of the
deployment pipeline and you’ve got “continuous architecture” that
evolves with guidance from the fitness functions.

The author’s make their case with examples and hypothetical case
studies. The author use a theoretical company called Penultimate
Widgets to demonstrate problems and throughout the text. Readers will
likely relate to hypothetical problems since they mirror frustration
in any software team.

## Thoughts

Many of the book’s ideas were not new to me. It seems natural to me
that software architecture is the discipline of managing technical
trade-offs, business outcomes, team structure, and hedging against
unknown unknowns.

I balanced this equation at Saltside best I could. I lead the team in
restructuring our quasi monolithic ball of mud into something more
service oriented / micro service architecture. We did this because
meaningful product development was too time consuming. This is a case
and point example of what happens when a team fails to evolve with
time. Interestingly enough, the restructuring steps we took are
mentioned in the migration case studies in later chapters so I guess
we did something right.

I did not make all the right decisions in that project. A few years of
long tail experience revealed new dimensions and brittle integration
points. Building Evolutionary Architectures may have helped cull those
effects, but that project completed years before the book was
published.

Personally, I did not get much out of the ideas discussed in the book
and few technical examples were not substantive enough for my taste.
However, I did appreciate the new vernacular because it provides a
great way to communicate aspects in software architecture.

The authors introduce catchy vernacular. This isn’t a slight. Their
vernacular is well thought out and useful. Let me begin with
“-ilities” — sort of like capabilities. Software architectures balance
“-ilities” such as “scalability”, “malleability”, or “debugability”. I
used the term “concerns” to cover these. Author’s sold me on
“-ilities” because it stands out from a myriad of other overloaded
terms.

They also introduce terms for classifying fitness functions. These
resonated with me the most since they enforce the trade-off spectrum
in all architecture decisions. They are (as quoted):

* Key: These dimensions are critical in making technology or design
  choices. More effort should be invested to explore design choices
  that make change around these elements significantly easier. For
  example, for a banking application, performance and resiliency are
  key dimensions.
* Relevant: These dimensions need to be considered at a feature level,
  but are unlikely to guide architecture choices. For example, code
  metrics around the quality of code base are important but not key.
* Not Relevant: Design and technology choices are not impacted by
  these types of dimensions. For example, process metrics such as
  cycle time (the amount of time to move from design to
  implementation, may be important in some ways but is irrelevant to
  architecture. As a result, fitness functions for it are not
  necessary).

It’s easy for me, in retrospective, to see what I classified as key,
relevant, and not relevant. Hopefully these terms stick with me for
use in future discussions.

I did pick up one powerful new idea. The author’s propose a form of
automatic dependency upgrades that minimizes technical debt.
Dependencies are marked as as “fluid” or “guarded”. Roughly speaking,
the deployment pipeline upgrades to the newest major or minor version
of fluid dependencies. If everything passes, then dependencies
automatically update. If they fail, then the process retires with a
minor version bump. If they fail again, then repeat with a patch
version bump. If they still fail, then they become “guarded” and
requiring manual action from engineers to restore the fluid label.

I think this practice would pay dividends for framework level
dependencies. They are the most painful because of higher coupling. If
you skip too many, then it becomes a massive task to get up-to-date.
Automated upgrades would mitigate technical debt and increase
security. Unfortunately there are no such tools available right now
for fluid and guarded dependencies.

## Highlights & Take-Aways

> Software architects should pay attention to how work is divided and
> delegated to align architectural goals with team structure.

The author’s devote a delightful amount of time to discussing the
connection between software architecture and team structure. Don’t
discount how architecture choices impact the flow of work and the
other way around. This is a powerful feedback loop which can destroy
companies!

> As developers restructure architecture, their first step should be
> to remove the historical design compromises that manifest as
> technical debt.

This is not obvious but important. It’s also nice to see that
technical debt is the manifestation of design choices (or “-ilities”
selection) that have become outdated.

## Recommendation

I recommend you skip the book. Instead visit the author’s websites,
listen to their conference talks, or podcast appearances. If you think
that software architecture should be flexibility and change over time,
and you have hands on experience in this domain then you may not get
much value out of the book. However, if you may find the book valuable
if you’ve never given high level architecture design much thought.
Even so, I think roughly the same information is available through
other free mediums.
