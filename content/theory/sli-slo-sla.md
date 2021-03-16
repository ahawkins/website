+++
author = "Adam Hawkins"
date = 2020-07-27T10:05:46Z
draft = false
summary = "SLIs, SLOs, and SLAs create a hierarchy. They measure reliability and create an objective framework for prioritization and decision making."
tags = ["SRE", "podcast"]
title = "SLIs, SLOs, & SLAs"
+++

## Podcast Episode

{{< transistor "https://share.transistor.fm/s/2d4241a3" >}}

_This is an episode transcript. Visit the [podcast
website](https://share.transistor.fm/s/2d4241a3) for the full episode,
show notes, and freebies._

Service level indicators, service level objectives, and service level
agreements create a hierarchy. Service level indicators define a
number. Service level objectives set a target for the number. Service
level agreements define rules and expectations for when the target is
hit or missed.

These are powerful tools for aligning stakeholders and determining
priorities. Each builds upon the other, so let's work bottom up
starting with service level indicators.

### SLIs

SLIs, or service level indicators, quantify aspects of the provided
service. Examples include latency, uptime, and error rate. Use this
template for defining SLIs: blank as measured by blank. Here's an
example: success rate as measured by the number of successful HTTP
requests divided the total HTTP requests. Express SLIs as ratios of
the total number of good divided by total number of events. This
provides a sliding scale between zero and one hundred.

There are infinite choices for SLIs, so they must be chosen carefully
to measure value of the provided service. Ask this question as a gut
check when considering an SLI: "will the service loose users if this
indicator is negative impacted?"

So what's the right number? This number is the SLO, or service level
objective. Clearly 0 is the wrong number because that means everything
is broken. On the other hand, 100% is not the right answer because
that means nothing every breaks. That's impossible. The real answer is
that it just depends on business.

### SLO

The SLO sits at the intersection of product and engineering.
Stakeholders must agree that if the SLO drops below a threshold then
it's worth reprioritizing work to reach the SLO. The means that
responsible party may commit to new work or eschew existing work to
maintain it. On the other hand, this means that work in ways to
maintain reliability so the SLO does not drop below the threshold in
the first place.

Once the SLO is defined, then the stakeholders can form an agreement
for how to maintain the SLO and what to do when it's missed. This is
the service level agreement or SLA. They typically take a form of
financial penalties or other negative consequences written into a
contract. These agreements are made between the consumer and provider.

However I'm focused on the agreement between those responsible for
maintaining the SLO. The site reliability engineering literature
recommends using an error budget for this.

Here's an example. Say the SLO is is 99% per quarter. That provides an
error budget of 1%. So, if a problem causes a failure rate of .5% then
50% of the error budget is used.

The error budget is an objective way to manage risk in relation to the
SLO. The team may decide to undertake a risky database migration when
the error budget is full. On the other hand the team may be more
conservative when the budget is low by focusing on low risk releases.
The error budget enables teams to balance risk, innovation, and
reliability. This assumes all stakeholder accept the error budget as
means of planning and maintaining the SLO. In other words, if the
error budget is exhausted then no releases may be possible. Are the
stakeholders OK with that?

That right there friends is the hard problem. Measuring something is
the easy problem. Giving the SLO power to change priorities is the
hard problem. That's why it's so important, and I cannot overstate
this enough, that the SLO directly relates to business success. It
needs teeth!

Many teams do not solve the hard problem. As a result the SLOs are
kabuki theater or relegated to some KPI spreadsheet. That's largely
been my experience. However I have had positive experiences with well
designed SLOs and an agreement to commit to them.

Lastly, I want to circle back to software delivery and the three ways
of DevOps.

SLIs & SLOs provide feedback to the software delivery process.
Feedback is the second way of DevOps. Teams cannot asses their
progress without feedback from production. SLOs provide feedback to
all stakeholders, be it engineers, business executives or product
managers. Feedback is the second half of the continuous delivery
cycle. Fast flow--A.K.A. continuous delivery--only happens with fast
feedback.

SLOs are not static either. They will change as the business changes.
Early stage businesses may accept more risk than established
businesses. Over time, systems may change to a point where maintaining
the SLOs has negative business impact. Maintaining SLOs is a never
ending balancing act that requires feedback from stakeholders and the
flexibility to improve them over time. This is an act of continuous
improvement--A.K.A the third way of DevOps.

Many topics in software delivery, release engineering, or site
reliability engineering connect back to SLOs, so don't forgo them.
They're mandatory for laddering up the SRE hierarchy of needs. Refer
to the SRE workbook and the SRE book for examples of determining,
defining, and implementing everything discussed in this episode.
