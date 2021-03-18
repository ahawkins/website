---
title: "Team Topologies"
subtitle: "Organizing Business and Technology Teams for Fast Flow"
edition: 1st
link: https://itrevolution.com/team-topologies/
cover: /images/team-topologies.jpg
date: 2019-09-17
publishDate: 2021-03-10
author:
  - Matthew Skelton
  - Manuel Pais
toc: true
tags:
  - devops
  - value streams
  - management
summary: |
  IT consultants Matthew Skelton and Manuel Pais share secrets of the
  four successful team patterns and three interactions modes to ensure
  success for IT organizations.
---

I've discussed Team Topolgies twice on Small Batches. The first is a
solo episode. I introduce the four team types and three interaction
models. The second episode is a conversation with Matthew Skelton.
Matthew and I discuss the book and inflections points in
organizational growth.

## Podcast Episode: Matthew Skelton

{{< transistor "https://share.transistor.fm/e/0f7015b2" >}}

## Podcast Episode: Team Topologies

{{< transistor "https://share.transistor.fm/e/8a037723" >}}

_What follows is a transcript of the podcast episode._

Hey there. Adam with for a solo episode of Small Batches.

Today I’m covering the 2019 book "Team Topologies: Organizing Business
& Technology Teams for Fast Flow" written by Matthew Skelton & Manuel
Pais.

Let me read off their official bio:

> Matthew Skelton and Manuel Pais - co-authors of the book Team
> Topologies - have worked together on organisation design for modern
> software systems with many clients around the world. Their training
> sessions on Organisation Design for Modern Software Systems have
> helped numerous organizations to re-think their approach to team
> intercommunication and software architecture, improving flow and the
> effectiveness of software delivery.

So I’m stoked to finally discuss Team Topologies on Small Batches.
This book has come up so many times in my work as an SRE at Skillshare
and tangentially related to everything I’ve discussed on Small Batches
to date. This is because team architecture and software delivery are
directly related to software delivery performance.

That’s particularly why I enjoyed Team Topologies so much because it’s
truly a book about high velocity software delivery. In fact it’s right
there smack in the title. Plus it provides a language to discuss this
facet of software delivery.

You’ve likely encountered some of these concepts before, so this time
around it may just be a new language.

I’ll share a personal anecdote from earlier in my career to set the
stage for this episode.

Roughly fives years ago I lead the platform team through a complete
ground up rewrite at a previous company. We were divided into
technology teams: The web, mobile, and platform team. Given these
boundaries each of respective team lead set out to create their
internal architecture. Nothing to see here: just Conway’s law in
action. It worked well here because we had isomorphic technology and
team architecture.

Then something happened out of the blue shortly after the rewrite
completed.

The organization went through a total re-org that changed the team
structure, their responsibilities and how they interacted without
doing anything to address the underlying technical architecture. This
created confusing boundaries, ownership responsibilities, and left so
called "independent feature teams" at the mercy of the small number of
capable backend engineers capable of working across the various
internal services.

These problems could have been avoided with some foresight and
planning. Plus it’s especially bothersome because the entire
engineering team had just finished a ground up rewrite that
architected a system to support an entirely different team topology!
If there was ever a time for a reverse Conway maneuver that was not
it.

This example speaks to the importance of Conway’s law and how team and
software architecture fit together to create fast flow or on the other
hand just inhibit it.

Team Topologies provides a framework that avoids this problem from the
outset by optimizing for fast flow. Alright, let’s get stuck in.

### Summary

Team Topologies addresses the relationship between software delivery
and team structure. The book's thesis is that team's are the means of
software delivery, so organizations must structure teams for fast
flow.

The term "topologies" refers to both the structure and dynamics in an
organization. Imagine a running river. Structure is like the rocks,
logs, and plants along the river's path. Dynamics is how water flows
and moves between the rocks, logs, and plants. The water may take a
different path as conditions change. That's the dynamics at play as
water navigates the river's structure. Organizations must consider
both structure and dynamics when constructing their team topologies.

All of this is in separable from Conway's law. Conway's Law asserts
that organizations are constrained to produce application designs
which are copies of their communication structures. This often leads
to unintended friction points when organizational structure butts u
against technological architecture. The "Inverse Conway Maneuver"
seeks to avoid this problem by evolving your team and organizational
structure to promote your desired architecture.

Team Topologies defines team as a stable group of five to nine people
working towards a shared goal as a unit. Teams may be responsible for
different parts of the software system, however different parts of the
software system are owned by exactly one team. This means there should
be no shared ownership of components, libraries, or code. Teams may
use shared services at runtime, but every running service,
application, or subsystem is owned by only one team.

The corollary is that ownership increases cognitive load. Cognitive
load is all the "stuff" that teams must keep in their head to
effectively build, deploy, and operate their services. Cognitive load
must be throttled to keep teams running effectively. Team Topologies
recommends limiting teams to two to three domains but never two
complex domains. The key is balancing the cognitive load against the
team's ability to respond to work in a timely fashion.

These "domains" relate to the team's position in the value stream.
Some people are better suited to making user facing software. Some
people are great a building infrastructure. Some people love sales.
Other write documentation or handle frontline customer support. This
position in the value stream impacts how they interact with other
teams. This is where we get to the meat of Team Topologies.

Team Topologies provides four fundamental team types:

1. stream-aligned
2. platform
3. enabling
4. and complicated-subsystem

Along with three team interaction modes:

1. collaboration
2. X-as-a-Service
3. facilitating

Let's begin with the team types then cover the interaction modes.

### Stream Aligned Team

A "stream" is the continuous flow of work aligned with a business
domain or organizational capability. Continuous flow requires clear
purpose and responsibility so that multiple teams can coexist, each
with their own flow of work.

A stream-aligned team is a team aligned to a single, valuable stream
of work; this might be a single product or service, a single set of
features, a single user journey, or a single user persona.

These teams are nimble. They can quickly change course and integrate
feedback into their work. More importantly, only they are on the
critical path to completing their work. This means zero or minimal
hand-off to other teams.

These are the organization's primary teams, but they cannot exist in
the vacuum. Stream aligned teams have end-to-end responsibility for
completing their work, a.k.a you build it you run it.

Requiring the team to manage every technical aspect of that process
would create undue cognitive load, thus impairing the team. This is
where the other team types come in. Their core purpose is supporting
the stream aligned teams.

### Enabling Team

The enabling teams typically work closely with stream aligned teams.
Their job is to increase the autonomy of stream-aligned teams by
growing their capabilities with a focus on their problems first and
not the solutions. Think of them as "Technical Consulting Teams".
Their members tend to have specialist knowledge in their particular
domain.

These teams tend to focus on specific area like release engineering,
continuous delivery, or testing. They’re likely able to create
skeletons solutions that apply best practices for other teams to build
on.

However they are not the owners or permanent dependencies. If the
enabling team is doing its job well, then interaction will be short
lived and after bootstrapping the intended capability the may move on
to work with a different team.

### Complicated Subsystem

The complicated subsystem teams help shed load cognitive load from
stream aligned teams.

They’re created when the domain is complex enough to warrant
specialist knowledge to make any change to the subsystem. Think of
something like an operating system, container orchestration system, or
face recognition algorithm. These are sufficiently complex that deep
understanding is required to be productive when working in this
subsystem. Also note that clear boundaries between the complicated
subsystem and their consumers.

The important bit is these teams are created to offload cognitive load
from stream aligned teams, not by a desire to share a subsystem. For
this reason there should be a small number of complicated subsystem
teams and zero in some cases.

### Platform Team

The platform provides autonomy to the stream aligned teams. Platform is defined as:

> a foundation of self-service APIs, tools, services, knowledge and
> support which are arranged as a compelling internal product.
> Autonomous delivery teams can make use of the platform to deliver
> product features at a higher pace, with reduced coordination.

The platform team assumes the cognitive load that would have been
placed on the stream aligned team if they were tasked with building
everything themselves.

Platform teams are highly collaborative by their nature. They tend to
work closely with their users (i.e. the stream aligned teams) to build
tools that solve their problems.

Note that in large enough organizations the "platform team" may be a
team of teams. Imagine AWS. That’s a single platform composed of
stream aligned teams for individual services as well as their enabling
teams, complicated subsystem teams, and internal platform teams.

### Interaction Models

Team Topologies defines three interaction modes:

- Collaboration mode: two teams work together on a shared goal,
  particularly during discovery of new technology or approaches. The
  overhead is valuable due to the rapid pace of learning.
- X-as-a-Service mode: one team consumes something provided by another
  team (such as an API, a tool, or a full software product).
  Collaboration is minimal.
- Facilitating mode: one team (usually an enabling team) facilitates
  another team in learning or adopting a new approach.

Different team types prefer certain interaction models. Stream-aligned
teams use X-as-a-Service or collaboration; enabling teams use
facilitation; complicated-subsystem teams use X-as-a-Service; platform
teams use X-as-a-Service for teams that consume the platform.

I recommend you check out the show notes for links to infographics and
presentations. This information is better digested some visual aids.
The book includes examples of many common scenarios and anti-patterns
in team structure and interaction modes. So my brief summary will have
to do for now.

### Fracture Planes

Organizations should adopt a teams first model then design teams
accounting for cognitive load and boundaries. This may be done using
what the author’s call "fracture planes".

The first fracture plane is business bounded domain context. This is
similar to what you’ll find in Domain Driven Design.

The next plane is regulatory compliance. This a natural boundary
because regulatory compliance tends to form firewalls in
organizations. This often requires specialized knowledge as well that
would only add cognitive load on other teams.

Third is change cadence. Certain areas of the organization move faster
or slower than others. This allows teams to adopt cadences that best
suite their work, say a maintenance stream aligned team compared to a
high velocity product stream aligned team.

Then comes location, or geography. Some things work better co-located
in an office, some things can be done distributed, that and each
person has their own preferences. One example is a globally
distributed "follow the sun" SRE team where members can be on-call
during normal working hours.

The fifth plane is risk. Differentiating risk profiles allows mapping
the technology changes to business appetite or regulatory needs. It
also allows each subsystem to evolve its own risk profile over time,
adopting practices like continuous delivery that allow increasing
speed of change without incurring more risk.

Next is performance isolation. This is similar to risk. Different
subsystem have different performance requirements. A real time video
streaming system is different than an SMS delivery API. Each requires
a different set of skills and different SLOs.

The seventh plane is technology. This is the classic separation and
may likely be avoided by using the other fracture plans. This plane
tends to focus on the "how" rather than the "why". However this useful
when dealing is older technologies that don’t play by the same rules
as others. I’m looking at you COBOL.

The final plane is user personas. A good example our enterprise
customers of a SaaS. Those users have different needs and pay
different rates. Splitting a team around supporting them provides
clear ownership of how those users succeed with a product or services.
Odds are your marketing teams has a few personas you can start with.

### Wrap Up

All of these are factors in determining team architecture. Here’s the
key quote to remember in that decision making process:

> Overall, the Team Topologies approach advocates for organization
> design that optimizes for flow of change and feedback from running
> systems. This requires restricting cognitive load on teams and
> explicitly designing the intercommunications between them to help
> produce the software-systems architecture that we need.

So that’s Team Topologies in a nutshell. This book changed the way I
think about the relationship between team architecture and software
delivery and overall impact on software delivery performance. It’s now
permeated my subconscious in a way that I cannot unsee it. That’s why
I wanted to share it with you. Perhaps it has the same effect.
