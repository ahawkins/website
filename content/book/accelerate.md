---
title: "Accelerate"
subtitle: "The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations"
link: https://itrevolution.com/book/accelerate/
cover: /images/accelerate.jpg
date: 2018-04-27
publishDate: "2018-04-29T00:00:00Z"
author:
  - Nicole Forsgren
  - Jez Humble
  - Gene Kim
tags:
  - devops
  - value streams
  - theory
  - leadership
  - management
toc: true
summary: |
  Accelerate measures software delivery performance—and what drives
  it—using four years of groundbreaking research and rigorous
  statistical methods.
---

I was excited when Accelerates was released. Their last book, [The
DevOps Handbook]({{< relref "the-devops-handbook" >}}), laid out a
repeatable path for moving towards the DevOps value stream.

I didn’t know what expect from Accelerate, but I hoped the authors
would delight me again. This review includes my thoughts, highlights,
and lastly a recommendation on who it’s best for. Skip to the end if
you’re just interested in the recommendation.

## Background

There has been hand-wavy correlation between DevOps and high
performance that tends to come across as marketing fluff. Accelerate’s
goal is to replace the fluff with facts by demonstrating the science
behind building high performing IT organizations.

High performing means delivering more value more quickly. Or in other
words, the ability to ship higher quality changes more frequently. The
book covers how teams achieve this from commit to production. The
entire software development process is omitted from the book.

Part 1 covers findings. Part 2 documents the science. Part 3 is a case
study in transformation from ING. There’a also summaries in the
appendixes.

## Thoughts

I read Accelerate after the DevOps Handbook. Accelerate felt like a
large appendix to the DevOps Handbook. This isn’t surprising given
it’s the same authors discussing the same topic with roughly the same
data. Generally speaking part one did not contain new conclusions or
ground breaking revelations. It felt like Accelerate provided more
ammunition for proponents of DevOps practices.

Accelerate puts a finger on measuring software delivery performance.
This a fuzzy problem since feel like part of a high performing, but
it’s challenging to compare performance across teams for a multitude
of reasons. Their measurement works around these problem with directly
observable metrics and inferred metrics. They break software delivery
performance into four metrics:

1. Lead Time: time it takes to go from a customer making a request to
   the request being satisfied.
2. Deployment Frequency: frequency as a proxy for batch size since it
   is easy to measure and typically has low variability. In other
   words: smaller batches correlates with higher deploy frequency.
3. Mean Time to Restore (MTTR): given software failures are expected,
   it makes more sense to measure how quickly teams recover from
   failure.
4. Change Fail Percentage: a proxy measure for quality throughout the
   process

I bet it’s intuitive what are better values for each of these metrics.
Obviously high performing teams satisfy customer requests faster,
while doing it more often, recover from failure faster, and fail less.
Accelerate provides values for high, medium, and low performers across
all the metrics.

That set of metrics and the discussion around them was worth the cost
of admission for me. I’ve shared the metrics but not the discussion of
why and how they relate to each other — that’s what the book is for
and the author’s do a much better job than I could.

Accelerate covers more than those four metrics. I found the
organization structure analysis interesting, especially since it was
measurable and correlated with other positive indicators. There’s also
information on leadership and employee satisfaction. I didn’t expect
the discussion of employee satisfaction, but the data shows that good
values on these metrics correlate with less burnout. Anyone (my self
included) who’s been through burnout knows that it’s horrible and
should be avoided.

I struggled finding satisfaction in my work as an engineering and also
creating a fulfilling work environment for my team as an engineering
manager. My operating mode was try to ship useful everyday. That way
you accomplish something each useful each day. Accelerate’s findings
corroborate my approach. It’s nice to know that there’s a better long
term solution than providing pizza and beer.

Accelerate addresses the leadership gap in the DevOps Handbook. I
didn’t recognize the gap until reading other material. The DevOps
Handbook doesn’t address the importance of leadership and
organizational support. I was pleasantly surprised to see this
discussed, with backing data, in Accelerate.

## Highlights & Take-aways

> This huge increase in responsiveness does not come at a cost in
> stability, since these organizations find their updates cause
> failures at a fraction of the rate of their less-performing peers,
> and these failures are usually fixed within the hour. Their evidence
> refutes the bimodal IT notion that you have to choose between speed
> and stability — instead, speed depends on stability, so good IT
> practices give you both.

So finally, once and for all, we can all say that you don’t have
choose between speed and quality. This is just more ammunition in the
fight for moving organizations toward the DevOps value stream. Please
take this to your team if you’re still in this fight.

> The moral of the story, borne out in the data, is this: improvements
> in software delivery are possible for every team and in every
> company, as long as leadership provides consistent
> support — including time, actions, and resources — demonstrating a
> true commitment to improvement, and as long as team members commit
> themselves to the work.

Improving the four metrics is possible for all IT companies including
those “stubborn enterprises”. There’s more on this in the book.
There’s no technical show stoppers, only people.

> It’s interesting to note that having automated tests primarily
> created and maintained either by QA or an outsourced party is not
> correlated with IT performance.

Take this one to your team if you’re fighting this battle. I’ve
experience this one first hand, so now there’s data on my side.
There’s another related point in the book that having an external
change approvable board (CAB) negatively correlates with IT
performance. The point is things you may think are improving
performance are at best creating toil and at worst hurting
performance.

> It’s possible to achieve these characteristics even with packaged
> software and “legacy” mainframe systems — and, conversely, employing
> the latest whizzy microservices architecture deployed on containers
> is no guarantee of higher performance if you ignore these
> characteristics.

This passage gave me chuckle (besides when Martin Fowler wrote
“bullshit masquerading as science” in the foreword) since teams adopt
technologies or architectures to achieve IT performance. In fact,
there are no findings of correlations between specific technologies
and IT performance. Practices are all the matter which are orthogonal
to technologies.

## Recommendation

Accelerate is an easy read which you can get through in 4–5 hours.
Reading the figures and tables on my Kindle was frustrating to the
point that switched to Kindle for MacOS instead. You can discern them
on the Kindle but it’s much easier on a better screen. The tables and
figures are discussed in the text so you can (like I did) make do
without seeing them clearly.

I recommend this book to decision makers wondering how to improve
their organization’s IT performance. If you enjoy statistics and
correlations then Accelerate makes a strong case for improving IT
performance by applying technical and organizational practices.
However you’ll be left wanting if you prefer case studies and personal
experience. Granted part 3 is dedicated to this, but it’s not
interwoven into the findings.

I also recommend this book to anyone trying to convince their
leadership to try DevOps practices. The data makes a strong case. Also
the gap between high and low performers is widening because the high
performance get better and low performers don’t. Push this book up the
chain of command sooner than later.

I do not recommend this book if you’ve already decided to move towards
DevOps and need a guide on how to get there. The DevOps Handbook is
far better suited and draws upon the same data with more first hand
experience and implementation patterns.

You’ll probably enjoy Accelerate if you’re passionate software
engineering and curious on how to improve the process.
