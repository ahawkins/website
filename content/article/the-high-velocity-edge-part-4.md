---
title: "The High Velocity Edge: Part 4"
author: "Adam Hawkins"
date: 2021-04-06T07:19:29-10:00
tags:
  - continuous improvement
  - toyota
  - devops
series:
  - The High Velocity Edge
summary: |
  Introducing Taiichi Ohno and the pull-based work philosophy
  known as "Kanban".
---

Welcome to part four of a series on Steven Spear’s 2009 book [The High
Velocity Edge][book]. Today, I'll discuss the philosophy behind the first
capability: design and operate systems to reveal problems when they
occur.

The philosophy originates from two pivotal figures in manufacturing
history: Sakichi Toyoda and Taiichi Ohno. Sakichi Toyoda founded
Toyota. Taiichi Ohno transformed manufacturing while working at
Toyota.

Taiichi Ohno set the vision for design. Sakichi Toyoda set the vision
for operation. These two men pioneered what we call "lean
manufacturing", which went on to become one pillar of the legendary
Toyota Production System.

Much of the philosophy behind high performance software delivery is
rooted in lean manufacturing. There’s a straight line from building
cars on an assembly line to software delivery practices like
continuous integration and continuous delivery.

The High Velocity Edge contextualized ideas and practices in the
DevOps Handbook for me. It also connected pathways in my own mind
around my own goals and patterns.

Again, this traces back to Toyota because–for whatever reason–Toyota
figured how to do everything faster, better, and more profitable than
everyone else. The High Velocity Edge is jam packed with examples from
the daily work at Toyota, especially for demonstrating the four
capabilities in action.

The next few episodes cover the most exciting and interesting chapters
in the book. These are the episodes I’m the most excited to share with
you.

These chapters are why I consider The High Velocity Edge one the most
important books I’ve ever read. It gave me the framework to
contextualize my work in service to a larger whole. I hope these
episodes does the same for you.

I say "in service to a larger whole" because the idea comes from the
legendary Taiichi Ohno.

Taiichi Ohno created the "kanban" pull based system at Toyota. His
objective was to ensure pieces of a larger whole harmoniously
synchronized rather than create discord.

Ohno developed a simple rule for this: If someone—(i.e. the
“customer”)—needed something, they had to ask for it, and the supplier
was not allowed to produce and deliver something until asked. This
ensures all work is ultimately linked to the end customer and
minimizes waste.

Spear described Ohno's vision for kanban as "everything always in
service to a unified whole". I'd never heard kanban explained like
this. To me, kanban was just "cards on a board moving from left to
right". This description helped me internalize one of Ohno’s profound
insights: only do work if asked. Here’s my example.

I work as an SRE, so my customers are other developers. My team had
been building out features for our internal platform, then _pushing_
work on other teams to adopt it. You may already be thinking this
sounds off. It was.

The result was work either went unused or shelved because our
customers either didn’t have the capacity to take on new work or
weren't ready for them. In short, they never asked for it.

Toyota has a term for this: "muda". Muda is anything that takes time
and does not add value for your customer.

Well _no wonder_ this wasn't working. Most of the work was pure waste.
Beyond that, it was frustrating to see our work unused or scrapped.
When I realized this, I stopped any work that was not explicitly asked
for by customers. I encouraged my teammates to do the same.

The result was less work in progress and more capacity for pull based
work. Now the team only pulls from other teams. If there’s nothing to
pull, then we work on internal technical debt and maintenance. That
delivers value to _us_ without pushing work onto our customers.

Spear's description of Kanban as "always in service to a unified
whole" plus my real world experience clarified the meaning by
"just-in-time". I could do an entire series of episodes on Taiichi
Ohno, kanban, and the Toyota Production System, but a single episode
will have to do for now.

Taiichi Ohno demonstrated how to design systems. We’ll see how Sakichi
Toyoda demonstrated how to operate them in the next episode. Until
then, I recommend you read the wikipedia pages for [Taiichi
Ohno](https://en.wikipedia.org/wiki/Taiichi_Ohno) and the [Toyota
Production System](https://en.wikipedia.org/wiki/Toyota_Production_System).
They're gifts that keep on giving.

[book]: {{< ref "/book/the-high-velocity-edge" >}}
