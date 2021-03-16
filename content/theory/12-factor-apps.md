+++
author = "Adam Hawkins"
date = 2020-04-21T03:25:45Z
draft = false
summary = "The 12 factor app sets guidelines for designing software for deployment pipelines. They're a great starting point that can be improved upon."
tags = ["podcast", "architecture"]
title = "12 Factor Apps"
series = [ "12.1 Factor Apps" ]
toc = true
+++

## Podcast Episode

{{< transistor "https://share.transistor.fm/s/6d84c28a" >}}

_This is an episode transcript. Visit the [podcast
website](https://share.transistor.fm/s/6d84c28a) for the full episode,
show notes, and freebies._

The 12 factor app describe how to build software for deployment
pipelines. These guidelines make software easier to run in
development, staging, production, and any future environment. Heroku
members wrote "The 12 Factor App" in 2012. The authors tried to
enumerate best practices for running applications on their platform.
These guidelines were especially helpful since they coincided with an
industry shift towards DevOps, micro services, and continuous
delivery.

The 12 factor app guidelines still relevant today since many software
teams are building distributed systems, which require attention to
detail as to how services are coupled, configured, and deployed. The
12 factor app is a wonderful starting point for best practices. In my
experience though they omit a few facets and leave room for
antipatterns in certain facets.

My goal with this podcast is to share knowledge and practices for
building, deploying, and operating software. The 12 factor app
triangulates all three of those areas. This is partially why I love
the 12 factor app so much. It’s a rare piece of work that hits on so
many themes of this podcast. In this episode let’s review the 12
factor app and flag future discussion points.

### Codebase

Codebase, the first factor, defines the relation between code, apps,
and deployments. The gist is that there is a single codebase (i.e. a
git repo) equates to a single deployed app (or service). Different
versions of a codebase may be deployed to different environments. This
implies that if there are multiple codebases, it’s not an app; It’s a
distributed system. Each component in a distributed system is an app,
which should also comply with twelve-factor. Let’s flag this for
future episodes, since we need to adopt a distributed systems first
perspective instead of the other way around.

### Dependencies

Dependencies, the second factor, states a twelve-factor app never
relies on system wide packages. Instead, apps must leverage tools like
Ruby’s bundler or Python’s virtualenv to manage their dependencies.
This is where the second factor ends. Separating out application
dependencies is just part of the problem. You must also isolate the
app’s runtime. Admittedly this is more relevant for Ruby, Python, or
Nodejs apps which rely on managed runtimes. The sticking point is the
same for statically complied applications say written in Go. Just to
reiterate, the "dependencies" factor focuses on application
dependencies rather than application runtimes or execution
environments. So where do those come from and what can deployment
pipelines expect from dependencies? Let’s flag this for future
episodes.

### Config

Config, the third factor, states the applications should read
configuration from environment variables. This makes it possible to
deploy changes to production without altering code. A litmus test for
whether an app has all config correctly factored out of the code is
whether the codebase could be made open source at any moment, without
compromising any credentials. Separating config and code is a great
start but not enough. Personally I find the third factor the most
wanting. There are great ways to work with config and horrible anti
patterns, neither are discussed in the third factor. Let’s stick a big
flag in this factor for discussion in future episodes.

### Backing Services

Backing services, the fourth factor, states applications makes no
distinction between local and third party services.  Now for example
an application’s database and connection to external APIs are treated
in same way. The idea promotes loose coupling between apps and
services. The 12 factor app uses an example of switching a local SMTP
service for a third party service with only config changes and no code
changes. Again, this is a good starting point but requires some
clarifications and to the config factor and future dev/prod parity
factor.

### Build

Build, release, run, the fifth factor, states apps use strict
separation between the build, run, and release stages. The build stage
converts code into an executable. The release stage combines the
executable and config into something runnable. In other words, a
"deploy" is the combination of code and config. It’s not possible to
change one without creating a new release.

### Processes

Processes, the sixth factor, states apps execute as one more stateless
processes using a shared nothing architecture. If data needs to
persist across restarts or releases, then it must be stored in a
stateful backing service such as a database. I like this factor
because it surfaces the idea that apps are composed of multiple
processes such as a web server, maybe a background job worker, or a
cron process. This model scales up to distributed systems which are
composed of multiple apps interacting across various processes. This
factor also implies the deployment pipeline must handle that releases
contain 1-N process which may require different semantics. In other
words, the deployment pipeline cannot assume a single process or
process type.

### Port Binding

Port binding, the seventh factor, states an app is completely self
contained and exposes itself through ports. This seems obvious but
it’s a good architectural principle to state out right. Given services
are exposed through ports, then it’s possible to configure others by
providing the hostname and port of relevant services.

### Processes

Processes, the eighth factor, state that processes are a first class
citizen. The stateless share nothing model naturally promotes
horizontal scaling. Just start more processes. Scale vertically by
allocating more resources to processes where need be. The corollary is
processes should never daemonize or write PID files. Instead they are
controlled process manager like systemd. In other words: write apps
that start processes in the foreground; use a process manager to
scale, start, and stop processes.

### Disposability

Disposability, the ninth factor, states processes should be ready to
start or stop a moment’s notice. Fast startup times encourages smooth
scaling. Conversely, processes must gracefully handle the `SIGTERM`
signal. Severs should stop listening on the relevant port, finish
processing any requests, then exit. This approach ensures new releases
or other infrastructure events do not impact user facing requests.

### Dev/Prod Parity

Dev/Prod parity, the tenth factor, states that apps are designed for
continuous deployment by minimizing the gap between development and
production.  The original guideline states: the twelve factor
developer resists the urge to use different backing services between
development and production. This makes sense when applied to databases
but has negative implications when applied to distributed systems.
Does this mean a development environment for one service in a large
distributed system mandates running all other services? Well if you’re
targeting dev/prod parity then the answer may be yes. However
answering yes is not always practical. Consider the case where the
system in question is a single service. Then it’s simple enough to
achieve dev/prod parity. Now scale up. What about dev/prod parity with
N=5, 10, 20, 100? The tenth factor offers no advice or guidelines for
how handle inflection points as the system grows or which degrees of
dev/prod parity to consider.

### Logs

Logs, the eleventh factor, state that apps never concern itself with
routing or storage of its output stream. Instead all output should be
sent unbuffered to standard out. This works well in development
because developers can see output in their terminal. It also works
well in production since tools can capture output streams for
analytics and storage. Again the eleventh factor is a wonderful
starting point but needs to be improved upon for continuous delivery
and production operations. The eleventh factor does not cover what or
how things should be logged. In fact this only mention of telemetry—a
vital facet of continuous deployment largely uncovered by the 12
factor app.

### Admin Processes

Admin processes, the twelfth factor, state that admin work such a
migrating databases or other out-of-band work executes as a separate
process. Processes can be started using the same release (meaning the
same config and code). I don’t have more to stay about this factor so
let’s put a pin in it and wrap up.

Future episodes will dive deeper into the individual factors with a
focus on identifying and closing the gaps. My biggest gripe with the
12 factor app is around the config and dev/prod factors and the
overall omission of anything telemetry metrics related.

I’m curious about your experience with 12 factor apps. How has it
worked for you? What do you think it’s missing? Where could be
improved? Send your comments to hi@smallbatches.fm. Also, tell me what
you want covered in future episodes.

With that, I leave you to it. Good luck out there and happy shipping.
