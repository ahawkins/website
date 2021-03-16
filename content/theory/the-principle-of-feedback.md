+++
author = "Adam Hawkins"
date = 2020-03-23T18:13:01Z
draft = false
summary = "The Principle of Feedback, or the second way of DevOps, describes using right to left feedback in the value stream."
tags = ["devops", "podcast"]
title = "The Principle of Feedback"
series = [ "The Three Ways of DevOps" ]
+++

## Podcast Episode

{{< transistor "https://share.transistor.fm/s/b47c6bf1" >}}

This episode continues our discussion on the Three Ways of DevOps. The
previous episodes introduced DevOps, the "Three Ways", and the
flow-the first way. This episode covers the second way of DevOps:
Feedback.

The DevOps philosophy works by establishing ways of working that feed
back into each other. The first way establishes fast from flow
development to production, or in other words, high velocity.
Organizations can’t stop there. Imagine yourself driving a car but
with one catch: there’s no speedometer, fuel gauge, or other
indicators. You could accelerate to a point, but eventually you’d need
to know how fast you’re driving so you can speed up or slow down; or
you’d need to know how much fuel  is left so you can stop to fill up
or not.

This is the principal of feedback in action. We need telemetry about
our ongoing actions to make subsequent decisions. Driving a car
reliably without a gas gauge would be pretty hard. The same idea also
applies to software. Production systems provide a wealth of
information about them. Let’s call this information telemetry.
Telemetry may be time series data, alerts, or logs; it’s any data that
provides insight into operational conditions. Once teams have
telemetry, then they can use as the basis for subsequent development.

This usually take two forms: using telemetry to automatically detect
error conditions and page an engineer or as maintenance work.

Here’s an example of each: automated monitoring detects a critical job
hasn’t run in 48 hours then pages an engineer; Engineers observe
telemetry to detect increased memory then decide to allocate more
memory to prevent future out-of-memory errors.

Both these examples are technical. Teams tend to focus on these areas,
but they need to aim higher. The Principal of Feedback must be applied
to all layers in the value steam, so that means the business too.

Good businesses track their "success" metrics. They’re likely
enumerated by quarter in some huge Google Sheet. They’re numbers like
"new user signups", "monthly recurring revenue", or "minutes watched".
Management deeply cares about this telemetry since they driving short,
medium, and long term planning.

Plus, this telemetry has something that technical telemetry does not:
it’s much easier to understand. That makes it a rallying point for
more people in the organization. Let’s face it. It’s just harder to
rally an entire business behind"Let’s drop the frontend to backend
latency!" compared to "Let’s boost our signups!".

There’s another important point here: something may only be improve if
it’s measurable. This is where DevOps overlaps with the "Lean"
philosophy. I’d like do a future episode on lean because it’s so
powerful and fits nicely along side the second and third way of
DevOps. For now let’s focus on lean and it’s relation to the second
way of DevOps.

Lean proposes thinking about business as a series of hypothesis
validated by real world experience. A common example is first putting
up a landing page for a non-functional product, then seeing if the
landing page converts users. If the page converts users, then there is
interest so it’s worth subsequent experiments to further validate the
idea. If the page does not convert, then try something else. Repeat as
many times as necessary. This example demonstrates the principal of
feedback. In this example, the team is measuring the conversion rate,
then plotting a course according to empirical data.

I cannot over emphasize the importance of empirical data. If we are
not using empirical data then we’re effectively guessing—and that is
dangerous! Here’s one of my favorite passages from the DevOps
Handbook:

The outcomes of A/B tests are often startling. Ronny Kohavi,
Distinguished Engineer and General Manager of the Analysis and
Experimentation group at Microsoft, observed that after “evaluating
well-designed and executed experiments that were designed to improve a
key metric, only about one-third were successful at improving the key
metric!” In other words, two-thirds of features either have a
negligible impact or actually make things worse. Kohavi goes on to
note that all these features were originally thought to be reasonable,
good ideas, further elevating the need for user testing over intuition
and expert opinions.

Whoa, scary right! So, if Microsoft only had 1/3 success rate for well
designed experiments, imagine their luck if they were shooting from
the hip.

As scary as it seems, this is great rallying point for the principal
of feedback. The Principal of feedback calls for establishing
automated telemetry across all phases of the value stream—from
planing, development, and into production—so that teams can monitor
their health across the value steam, then ultimately their progress
towards business objectives. In other words, if teams have telemetry
about their current course, they’re able too—and hopefully more likely
too—take a step back and see if things are moving in the right
direction.

That’s a good stopping point because we can pick up this conversation
again with the Third Way of DevOps in the next episode. Head over the
podcast website smallbatches.dev for a transcript and show notes. If
you enjoyed this episode then please tweet it and share with your
friends and colleagues.

Until the next one, good luck our there and happing shipping. Adidos!
