---
title: "The High Velocity Edge: Part 1"
author: "Adam Hawkins"
date: 2021-03-20T15:40:30-10:00
tags:
  - continuous improvement
  - toyota
  - devops
series:
  - The High Velocity Edge
---

I'm taking Small Batches back to its roots for the next series of
episodes. I've written coffee cup size servings of software delivery
education based on Steven Spear's 2009 book [The High Velocity
Edge][book].

The High Velocity Edge offers a simple hypothesis: organization's with
higher learning velocity beat the competition. Today's organizations
are complex adaptive systems that fail in curious and unexpected ways.

This is evident in the story of Mrs. Grant.

Mrs. Grant was recovering from cardiac surgery in the hospital. The
day nurse discovered Mrs Grant having a seizure at 8:15 AM. A code was
called and blood work rushed the lab. Blood work revealed a undectably
low serum-glucose level. Mrs. Grant's brain was sputtering out like a
car on an empty tank.

Attempts to intervene intravenously failed. Her condition worsened
until she went into a coma. She died weeks later when she was taken
off life support.

What happened to Mrs. Grant?

The hospital conducted an immediate investigation. The investigation
showed a nurse responded to an alarm at 6:45 AM. The nurse diagnosed a
potentially fatal blood clot. The nurse injected a dose of the
anticoagulant herapin to break up the blood cot. The nurse left the
room when Mrs. Grant was resting peacefully.

How did she go from resting peacefully to on life support in under two
hours? Well, a minor detail and a frantic moment culminated to kill
Mrs Grant.

Heparin could saved Mrs Grant. Instead she was given a fatal dose of
insulin simply because the nurse grabbed the wrong vial.

The investigation found that both vials of insulin and herapin look
the same. Of course they're labeled differently, but the type is small
and specific details are even smaller.

We've all seen a nutrition information label or the list of
ingredients on a can of soup. Now shrink that down ten times. Too make
things worse, the vials were also placed close enough to each other so
one could be chosen by mistake.

That's exactly what happened. Sure the nurse may have correctly
identified herapin but combine that with someone in a rush, responding
to a critical alarm, in a dark room, and at end of the overnight
shift? Doubtful.

I can put myself in the nurse's shoes because I've done the same
thing. I've pushed code to production that was seemingly correct then
went about my business. Later things failed catastrophically.

Here's an example of a time that I killed Mrs. Grant.

I had just joined a new company. The standard onboarding process was
to ship a small change to production. I committed my code change then
completed the code review process. Engineers much more familiar with
the codebase approved my change. All systems were go so, I deployed my
change to production.

Immediately afterwards user records started deleting from
the database. Um, what? How _could I have done that?_ I _just_ changed
this small thing over here.

More experienced engineers stepped in and diagnosed the problem. My
change had a unexpected side effect that was not caught by the
existing test suite or code review. Some code path modified an
instance variable which triggered a code path that deleted data.
Unfortunately my code was executed on every request, so every request
deleted data from the system. I was killing Mrs Grant every time a
user visited our website.

Who's to blame for killing Mrs Grant and who's to blame for all that
deleted data? The nurse did what they were expected to do: give the
patient medicine known to prevent blood clots. I did what was expected
of me: test my change to the best my ability and have it reviewed my
those more knowledge than myself.

So who's fault is it then? Is it the pharmacy who arranged the vials?
Is it the code reviewers who didn't identify the fault? That's possible, but
what if _they too_ were just doing what was expected of them. In that
case, the process itself is the culprit.

If the process is the culprit then wouldn't people like Mrs Grant be
killed all the time or more bad changes go out to production?

Spear offers some research on the topic. Research showed that five to
ten patients are injured for every patient killed by an error in
medication administration, like the one that killed Mrs Grant. Then
for every injury, there are five to ten close calls (like identifying
the wrong medication before administering it). For every close call
there are five to ten slip-ups or mistakes.

If the same is true about software then five to ten people may have
also written code with unintended side effects. Then another five to
ten people would have realized their code had unintended side affects
before deploying to production. Then another five to ten would have
committed code that unintended side effects, of course some worse than
the others--detectable or not.

The truth is that there were hundreds, if not thousands, of
opportunities to save Mrs Grant.

All it takes is one person to say "Hey! Mixing up these vials could
kill someone. We need to do something about it." or "Wow! This code is
doing something unexpected. We need to make our system more
deterministic or add a test for this."

Sadly, that's not what happened. These cascading failure signals
indicated the process was inadequate and should be modified. Instead,
the failure signals were considered obstacles to overcome as normal
noise in the daily process.

Each person got _their_ job done but they did not increase the chance
that the next person would have a higher chance of success.

All these factors culminate in Lemony Snicket's type "Series of
Unfortunate" events.

So-called "High Velocity" organizations are different. They strive to
continuously reduce errors and increase failures through four
capabilities:

1. system design & operation
2. Problem solving & improvement
3. knowledge sharing
4. developing high velocity skills in others

We'll cover these in future episodes.

[book]: {{< ref "/book/the-high-velocity-edge" >}}
