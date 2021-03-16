---
title: "Software Development in 3 Principles and 4 Metrics"
date: 2020-03-09T23:59:08Z
series:
  - "The Three Ways of Devops"
draft: true
---

My career began as a web application developer. I assumed success
depended on choosing specific technologies. I leveled up with exposure
to different technologies, companies, roles, and perspectives. 10
years of experience refutes my assumption. Success does not depend on
specific technologies. It requires a value stream centric worldview
and continuous improvement.

You may implicitly understand this idea without grokking the concept.
Consider your own anecdotal experience. Which do you prefer: automated
deployments backed by automated tests or manual deployments backed by
manual testing? Pushing code changes to production every day or every
month? Using production telemetry to guide post-mortems or running
production blindly? Guessing what works in the product or validating
ideas with A/B tests? Aligning teams with shared goals or putting
teams at cross purposes? If your experiences are anything like mine,
then you have a preference (and happy memories of a great team if
you’re lucky but scar tissue from burnout and 3AM pages is more
likely).

Each questions covers a philosophical principal. The principles are
simple: Use fast feedback cycles then validate results with metrics.
Now you’re off to the races. This philosophy is called “DevOps”.

## The Value Stream World View

The value stream is the process for converting a business idea into a
technology enabled service that delivers value to the customer. We’ve
changed how we interact with the value stream as software
professionals and software consumers. Acceleration is the trend.

Different philosophies attempted to relate the value stream’s changing
nature. First Agile. Second lean. Third DevOps (and it’s cousins like
DevSecOps and NoOps). Agile covered software development. Lean
introduced ideas such as MVP’s, short cycle times, and hypothesis
driven development. DevOps uses these ideas and others as the basis
for technical practices.

## Leveraging Flow, Feedback, and Learning

The [three DevOps
principles](http://itrevolution.com/the-three-ways-principles-underpinning-devops/)
are:

1. strive for short cycle times from development and production
2. feedback information about production to drive development
3. experiment to improve theses processes.

Each principal creates its own feedback loops. The effectiveness of
each feedback loop is measured by four relevant metrics:

1. lead time
2. deployment frequency
3. MTTR (mean time to resolve)
4. change failure rate.

These three feedback loops and four metrics encapsulate the value
stream.

[The DevOps Handbook][] articulates the philosophy and practices.
[Accelerate: The Science of Lean Software and DevOps][accelerate] into
IT performance. Accelerate introduces the four metrics and frames
software delivery performance. More importantly, Accelerate presents
empirical evidence that implementing DevOps principles leads to more
competitive businesses, happier employees, and better software. In
other words, Accelerate validates this wonderful quote from The DevOps
Handbook’s conclusion:

> DevOps benefits all of us in the technology value stream, whether
> are are Dev, Ops, QA, InfoSec, Product Owners, or customers. It
> brings joy back to developing great products with fewer death
> marches. It enables humane work conditions with fewer weekends and
> missed holidays with our loved ones. It enables teams to work
> together to survive, learn, thrive, delight our customers, and help
> our organization succeed.

Let’s begin with the feedback loop center to the software value
streams: the process to push committed code into production.

## Flow as Measured by Lead Time and Deployment Frequency

> The principle of flow enables fast left-to-right flow of work from
> Development to Operations to the customer. In order to maximize
> flow, we need to make work visible, reduce our batch sizes and
> intervals of work, build in quality by preventing defects from being
> passed to downstream work centers, and constantly optimize for the
> global goals.

The idea is reduce the time between committing code and that code
running in production without causing chaos or disrupting customers in
production. This measurement is “lead time”. Accelerate defines “lead
time” as:

> the time it takes for work to be implemented, tested, and delivered

Short lead times are better because that means the team is fulfilling
more requests (as features or bug fixes). In other words: the value
stream delivers value more quickly. Striving for short lead time is
critical because production is the only place where code provides
business value. Customers don’t care a lick for code in topic
branches. They care if they can use it. That only happens in
production, so the faster items flow from development to production
the better. This feeds back into the second principle since production
is the only place to truly learn about the business or product.

Assuming a team has short lead times, then it follows they deploy
frequently. Deploy frequency is a proxy measurement for batch size.
Consider batch size as the code diff between releases. Striving for
short lead times encourages smaller batches since they are easier to
develop, test, and deploy. Together lead time and deploy frequency
measure velocity.

The software development lifecycle does not end when code enters
production—that’s where it _begins_. Usage patterns change, there’s
SLO to achieve, outages to resolve, and business ideas to validate.
Teams need feedback from production to drive subsequent decisions.

## Feedback as measured by MTTR

> The principle of Feedback enables the fast and constant flow of
> feedback from right to left at all stages of our value stream. It
> requires that we amplify feedback to prevent problems from happening
> again, or enable faster detection and recovery.

The above quote is taken from introduction to the DevOps Handbook. The
idea is to provide feedback via telemetry about all parts of the value
stream. This includes the deployment pipeline itself, infrastructure
data such memory usage or CPU load, and product metrics like active
users and engagement.

Hypothesis validation and learning is the prime focus. Building
telemetry into the value stream sets a foundation for aligning the
team to shared goals (such as improving lead lead times or increasing
revenue) and for achieving organization goals. It comes down to this:
if something cannot be measured, then it cannot be tracked. If
something cannot be tracked, then it cannot be improved. Luckily, this
is not the case. The mean-time-to-resolve (MTTR) metric captures
effectiveness in the value stream’s telemetry systems.

We’ve covered three metrics so far: Lead time, deployment frequency,
and MTTR. Organizations want short lead times and more frequent
deploys. Organizations want lower MTTR since that implies negative
consequences in production are dealt with quickly, which reduces
business impact.

The principles of flow and feedback establish two feedback loops. The
first from development to production. The second from production to
development. Again, the software development lifecycle does not stop
there. The business and technology landscape is constantly changing.

## Learning as measured by Change Failure Rate

> The [principle of learning][toyota kata] enables the creation of a
> generative, high-trust culture that supports a dynamic, disciplined,
> and scientific approach to experimentation and risk-taking,
> facilitating the creation of organizational learning, both from our
> successes and failures.

Faster cycle times are a recurring theme. It applies to learning
opportunities as well. The above quote from The DevOps Handbook speaks
to organizational culture. Organizations should strive to create more
learning opportunities earlier in the process (akin to “shift left”).
When done right, this fosters a culture of experimentation that
enables improvement from all participants in the value stream.

This is evident in the fourth and final metric: change failure
frequency. Change failure frequency is the percentage of changes that
have any negative consequence in production such as outage or that
require corrective action.

I offer a different interpretation focused on hypothesis driven
development. A change is considered a failure if it does not validate
our hypothesis. It’s given that a particular change will not create an
outage or other negative consequence. If that does happen then that’s
an obvious failure. However we must expand our definition to account
for _why_ the team choose to make a change. If the team expects a
conversion rate X on a given feature and does not achieve it, then
that’s a failure. It’s likely not a technical failure, but a failure
in the value stream itself.

Considering a change a failure for not achieving a specific conversion
rate may some far fetched but thinking this way is possible. The
definition of “failure” may adapt over time as the value stream
matures. Applying a continuous improvement philosophy encourages the
organization to identify increasingly faint failure signals then work
to guard against them.

Failure signals are not confined to technical details. The business
process can (and often does) fail as well. A culture of continuous
learning treats the missed conversion rate as a learning opportunity.
Perhaps the idea was not properly A/B tested before committing to a
full implementation. Perhaps the design wasn’t aligned with existing
expectations. Perhaps the price was too high. The answer to this is
irrelevant in this scenario. The relevant question is why did it
happen and what can be done in the future to prevent it? This
philosophy keeps businesses ahead. Or as Peter Senge puts it:

> The only sustainable competitive advantage is an organization’s ability to learn faster than the competition.

## Conclusion

The principles of flow, feedback, and learning provide a philosophical
framework for understanding the technology value stream. The power in
these principles is not confined to software development.

Mik Kersten’s "[Project to Product][]" introduces the Flow Framework.
The Flow Framework applies the three principles to the entire
businesses. The Flow Framwork models relationship between all value
streams in a business, feedback between them, the value ultimately
produced for the consumer.

The power in these principles is not tied to specific technologies or
industries either. Accelerate states this explicitly:

> The moral of the story, borne out in the data, is this: improvements
> in software delivery are possible for every team and in every
> company, as long as leadership provides consistent support—
> including time, actions, and resources—demonstrating a true
> commitment to improvement, and as long as team members commit
> themselves to the work.

Businesses can apply these ideas _today_ and make a difference in
their value stream. In fact, they should probably start _now_ because
the highest performing businesses are already using the continuous
learning feedback loop to get better. In other words, the gap is
widening between top and bottom performers.

Accelerate finds the best performing teams have lead times under an
hour, deploy on demand, under an hour MTTR, and a 0-15% change failure
rate. They’re doing this with continuous delivery, continuous
integration, trunk-based development, automated telemetry, and
continuous learning-or what we refer to as “DevOps”. The three
principles establish a framework for thinking about these metrics, why
they’re important, and how to improve them irrespective to your
position in the value stream. That’s software development in a
nutshell.

[the devops handbook]: {{< ref "book/the-devops-handbook" >}}
[accelerate]: {{< ref "book/accelerate" >}}
[project to product]: {{< ref "book/project-to-product" >}}
[toyota kata]: {{< ref "book/the-toyota-kata" >}}
