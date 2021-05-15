---
title: "The High Velocity Edge: Part 6"
author: "Adam Hawkins"
date: 2021-05-09T14:47:03-10:00
tags:
  - continuous improvement
  - toyota
  - devops
series:
  - The High Velocity Edge
summary: |
  How kanban and jidoka create a framework for system design and
  operation.
---

Welcome to part six of a series on Steven Spear’s 2009 book [The High
Velocity Edge][book]. Today, I’ll discuss how kanban applies to system design
and jidoka applies to system operations. Together they create a
framework for system design and operation.

Every system may treated like a black box. There are inputs one side
and outputs on the other. The system's purpose is to deliver the
output. That's the objective. That's the thing that delivers value.
It's also the thing that defines success or failure.

Specifying outputs is the first level of system design.

A Kanban pull-based system matches demand with output. So, the system
should only produce output if requested by the consumer. This ensures
that all work done by the system is in service to the outputs.

[Jidoka][] means self-regulation using built-in checks. The built-in
checks for this level check the match between output and demand. If
the system is overproducing, then that’s waste. If the system is
underproducing then it’s lacking resources.

Now peek inside the black box. What's happening to deliver the
outputs?

You'll see pathways for material, information, and services that
convert the inputs to outputs. Ideally in a linear flow with minimal
hand-offs, exchanges, and feedback loops.

Imagine this like the different roles in an organization. There are
executives, managers, programmers, marketers, and customer support.
Inputs will flow through each of these people before becoming an
output.

Each person pulls work as needed, then signaling other when their work
completes. Built-in checks indicate problems with linear flow,
unexpected interrupts, or idle people.

If people are interrupted, then that indicates low resources. If
people are unexpectedly idle then that indicates over design or is
over provisioning. Do you see how problems at this level bubble up to
mismatch demand and capacity?

Now look one level deeper. Each pathway in the system has it's own
inputs and outputs.

Product managers use research to write user stories for programmers.

Assembly line workers use nuts and bolts to attach tires for a
customer's new car.

Waiters convert customer orders to chef friendly instructions.

Each of these requests and responses have their own requirements for
material, information, and services. The built-in check for the
request answers this question: do I have everything I need to produce
the output? The built-in check on the response answers the question:
is everything I've produced useable by my consumer? Applying Jidoka
here builds quality control into operations.

Cooks do this naturally. First they check they have everything
required for the recipe before starting. Then, they frequently check
their work by tasting it, only putting it on the table when it's
ready.

Engineers apply the same principle to deployment pipelines by
including [preflight checks][] that prevent deploys in known failure
conditions and using smoke tests to quickly check that system is
usable by consumers.

The "percent complete; percent accurate" metrics applies here. It
captures the output quality of each connection in the system. Quality
problems may be identified before they infect downstream consumers.

Quality control in operations is not enough. The system must also
match demand with capacity.

The hypothetical chef should only making dishes requested by someone
at a table. If food is piling up on the table, then there's a response
without a request. On the other hand, if hungry people are piling up,
then there's a request without a response. Each indicates a different
problem in the system's connections.

Let's follow our hypothetical chef into the kitchen. This where the
actual work happens. The chef follows a recipe to turn ingredients
into tasty meals. This activity is lowest level of system design.

Built-in checks indicate problems with the work itself. Say the recipe
isn't being followed. This may indicate a problem with the recipe
itself or the training to follow the recipe. What if the recipe is
being followed but there's still problems with the food? Well, then
there may be a problem with recipe.

Now, let's zoom all the way back out to where all we see is the black
box. These are the four levels of system design.

Level one: system output. What does the system have to deliver, to
whom, and by when to be successful?

Level two: pathway design. Who does what for whom?

Level three: Connection design, triggers and exchanges between
pathways.

Level four: Methods for individual task activities, basically how
tasks are done.

High velocity organizations apply these principles to design systems
that reveal operational problems as soon as they occur. This is the
first capability.

The second capability is actually solving the problems. That’s for the
next episode.

[book]: {{< ref "/book/the-high-velocity-edge" >}}
[preflight checks]: {{< ref "/theory/preflight-checks" >}}
[jidoka]: https://kanbanize.com/continuous-flow/jidoka
