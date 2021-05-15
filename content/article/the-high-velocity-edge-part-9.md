---
title: "The High Velocity Edge: Part 9"
author:  "Adam Hawkins"
date: 2021-05-15T13:04:33-10:00
tags:
  - continuous improvement
  - toyota
  - devops
series:
  - The High Velocity Edge
summary: |
  How the High Velocity Edge changed my thinking and work
---

Welcome to part nine of a series on Steven Spear’s 2009 book [The High
Velocity Edge][book]. This is the last episode in the series before my
interview with Dr. Spear. Today, I’ll wrap up with my closing thoughts
on the book and how it changed my work.

First, I think this is one of the most important books I’ve read.
That’s why I’ve done so many episodes on it. I read the book somewhere
around October or November of 2020. It’s now May 2021. That’s given me
plenty of time to digest the ideas, adopt some practices, explain them
to others, and really just change how I think about work itself.

The High Velocity Edge’s description of kanban and jidoka changed
everything for me. I’m glad that I read this book after spending so
much time on [The DevOps Handbook][], [Team Topologies][], [Accelerate][], and
Continuous Delivery. The High Velocity Edge gave me a framework to
integrate all the knowledge I had into a more consistent philosophy.
It also made even more admirable of Japanese culture and commitment to
decades long continuous improvement.

My biggest change was understanding why pull-based work is so
important. That portion of the book hit me hard. I realized that my
approach was pushed based. I was creating waste, frustrating others,
and leading to more work-in-progress. Team Topologies gave me the
terms to explain this to my team in the next team meeting.  We a
platform team. We cannot push work. We must only pull work that’s
requested from us from the product teams. That will reduce our
work-in-progress, cut waste, and cull our burnout--more importantly
give us the capacity to respond to real business demands. 

I could not communicate that until reading the High Velocity Edge.
Before, "kanban" was just cards on a board to me. Now I know it’s
deeper than that.

I also increased my focus on jidoka by adding more built-in checks to
every system I touched. This manifested itself in adding a lot of
assert statements to my Javascript. Sure asserts are not self
correcting, but they’re guaranteed to stop the program if something is
broken.

This was also inspired by a quote from Admiral Rickover about latent
assumptions. Code has many latent assumptions—especially dynamically
typed code, so don’t let them be latent. Make them explicit. You’ll be
surprised when those asserts fails because it reveals imperfect
knowledge. Plus, it will be much easier to troubleshoot failing
asserts than diagnose a bug much further downstream.

The High Velocity Edge also made me very curious about Taiichi Ohno,
Saikichi Toyoda, and Admiral Rickover. These are fascinating people
with stories and knowledge to share. I think it’s the first time that
I’ve been interested in specific people, and not just the ideas.
That’s a testament to the strength of their ideas and commitment to
them. 

I’ve done my best to share the best of the High Velocity Edge with you
in this series. There are more examples of each capability in the
book. There’s many from Toyota and for good reason. They get it. You
can learn from them. I know I did.

I’ll leave you with one last thing that wraps up the whole package.
The High Velocity Edge led to learn a lot more about Toyota. That led
me pick up the 2nd Edition of Jeffery’s Liker’s book [The Toyota
Way][]. The second edition was published this year so the information
is fresh. The book includes the eight steps of the Toyota Business
Practices:

1. Clarify the problem
2. Break down the problem
3. Set a target
4. Analyze the root cause
5. Develop countermeasures
6. See countermeasures through
7. Evaluate both results and processes
8. Standardize successful processes

Then I’ll add step 9: teach others to follow the previous steps

Alright that’s it for the series! Thanks for sticking with me this
far. Next episode features my conversation with Dr. Steven Spear.

[book]: {{< ref "book/the-high-velocity-edge" >}}
[The DevOps Handbook]: {{< ref "book/the-devops-handbook" >}}
[Accelerate]: {{< ref "book/accelerate" >}}
[Team Topologies]: {{< ref "book/team-topologies" >}}
[The Toyota Way]: https://www.amazon.com/Toyota-Way-Second-Management-Manufacturer-dp-1260468518/dp/1260468518/ref=dp_ob_title_bk
