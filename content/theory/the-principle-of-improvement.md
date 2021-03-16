
+++
author = "Adam Hawkins"
date = 2020-04-07T00:54:57Z
draft = false
summary = "A look into into how fostering a culture of experimentation and learning drive continuous improvement. This is known as the Third Way of DevOps."
tags = ["devops", "podcast"]
series = [ "The Three Ways of Devops" ]
title = "The Principle of Improvement"
+++

## Podcast Episode 

{{< transistor "https://share.transistor.fm/s/c5f31d67" >}}

This episode completes our introduction to the three ways of DevOps.
The previous two episodes introduced flow and feedback. Flow, the
first way, establishes fast left to right flow from development to
production. Feedback, the second way of DevOps, establishes right to
left feedback from production to development, so using the state of
production informs development decisions. The Third Way of DevOps,
establishes a culture of experimentation and learning around improving
flow and feedback.

Let’s frame this discussion using the four metrics from Accelerate:
lead time, deployment frequency, MTTR, and change failure rate. Lead
time and deployment frequency measure flow. MTTR measures feedback.
Change failure rate measures experimentation and learning. Trends in
these four metrics also reflect experimentation and learning.

Consider this scenario. There’s a severe 6 hour production outage. As
a result the business has lost money and received angry emails from
customers. This long outage window impacts the team’s MTTR. This
bug—undetected by the deployment pipeline—caused an outage which
increases the change failure rate. The team meets as soon as possible
after restoring production operations. What do they do? If they apply
the third way of DevOPs, then they would conduct a blameless
post-mortem. The post-mortem would identify the root cause of how this
bug entered production and what regressions tests to prevent it in the
future. Hopefully they also discuss why it took six hours to restore
operations and how they can be quicker next time around.

Here’s another scenario. A team ships new features on a regular basis
but they don’t see the expected business results. They thought these
features would deliver results but can’t figure out why they are not.
What can be done? First, the team needs to step back and check their
assumptions. Instead of going all in on big features, they can test
their assumptions with tiny experiments released to a small segment of
their users. If the results are positive, then the team should
continue iterating. If not, then the team tries a new idea. Over time
the team sees that they spend more time delivering on proven business
ideas instead of ideas they assumed would just work. This approach is
known as A/B testing or hypothesis-driven deployment from the lean IT
school.

Both scenarios demonstrate a focus on improvement through
experimentation and learning. However this only possible in a high
trust culture. It’s not possible to conduct a blameless post mortem if
people are afraid to say what they did to cause an outage. It’s not
possible to conduct A/B tests if the organization does not see the
value in validating business ideas through experiments. This is why
leadership must promote these idea. I’m going to read one of my
favorite passages from the DevOps Handbook. There are _many_ wonderful
passages in this book, but this is top tier without a doubt. The
passage is great example of leadership’s role:

> Internally, we described our goal as creating “buoys, not
> boundaries.” Instead of drawing hard boundaries that everyone has to
> stay within, we put buoys that indicate deep areas of the channel
> where you’re safe and supported. You can go past the buoys as long
> as you follow the organizational principles. After all, how are we
> ever going to see the next innovation that helps us win if we’re not
> exploring and testing at the edges?

I just love that quote—there’s just so much good stuff there. It
describes a high trust culture guided by safety and aligned through
principles. The four metrics (lead time, deployment frequency, MTTR,
and change failure rate) are SLI’s. DevOps is a set principles that
guide organizations to move those SLIs in the right direction, and
when done right the results are outstanding. You just need to ask how
can we improve? If you can stick to that then you’ll uncover that
improvement of daily work _is_ the daily work.

Alright, that’s it for principle of experimentation and learning.
These three ideas will come back all the time on the podcast, but hey
you always come back to these episodes if you need a refresh. Head
over to the podcast website smallbatches.dev for links and free ebook
on putting continuous improvement into practice.

Until the next one, good look out there and happy shipping!
