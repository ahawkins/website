+++
author = "Adam Hawkins"
date = 2020-06-29T21:03:45Z
summary = "Preflight checks prevent deploys into known bad conditions"
tags = ["podcast", "deployment pipeline"]
title = "Preflight Checks"
+++

{{< transistor "https://share.transistor.fm/s/8a6109a8" >}}

_This is an episode transcript. Visit the [podcast website](https://share.transistor.fm/s/8a6109a8) for the full episode, show notes, and freebies._

---

_Launch poll audio clip_

You just heard a NASA flight director run through a launch team poll.
The flight director asks each system asking for a go-no-go. All
systems must be go for the launch to continue. This practice is
critical because launching with the incorrect conditions may be
catastrophic. The same practice applies to deployment pipelines.

Deployment pipelines are a series of steps. Each step has three parts.
Step 1: Verify preconditions. Step 2: Do the work. This may be
initiating a rolling deploy, launching canary, or running a migration.
Step 3: Verify changes from step 2. This process mirrors the structure
in automated tests: establish preconditions, run code, then assert on
results. This approach provides three key benefits.

First, fail fast. It’s preferable to abort the pipeline early instead
of identifying a failure. Second, correctness is baked into the
pipeline. There’s no need to manually muck around after executing the
pipeline. If the pipeline completes successfully then you can say
confidently that the system is working. That’s the same feeling you
get from a strong test suite. Third: there’s a structure to
confidently grow and refactor  the pipeline. This is similar to the
"red-green-refactor" loop in TDD. So when regression is identified
then, it may be rooted out at step one or tested for in step three.

Preflight checks are the first step in a pipeline.  They are coarse
grained end-to-end tests that verify the pipeline may proceed.
Consider a typical application.

Typical applications use a database and some external services. Let’s
say the application uses PostreSQL and integrates with Twitter. This
implies at least two things:

1. The application can connect and authenticate to the PostgreSQL
   server
2. The application can connect and authenticate to Twitter If these
   preconditions are not met, then we know for certain there will be a
   production outage. The deploy pipeline must prevent shipping code
   when these preconditions are not.

These requirements start a list of preflight checks. Let’s assume that
connection and authentication information are provided via URL
environment variables in accordance with 12 factor app guidelines.

The first preflight check establishes a database connection to the
configured host & port, authenticates as the configured user, then
runs a simple query. Ideally this is executed via application code. If
that’s not possible then it may be done with the `psql` command.

The second preflight check authenticates with Twitter then executes an
operation part of the application’s normal operation. This may  be
fetching some tweets or loading a user’s profile. Ideally this is
executed via application code using the same libraries, such as an
OAuth client, and configuration as in production. If that’s not
possible then it may be done with a few `curl` commands.

The point of these tests is not specific assertions. The goal is to
check if something _is_ wrong. If these tests fail, then something is
critically wrong. What _is_ wrong is up to developers to suss out.
This is simply the nature of end-to-end tests. There are infinite
reasons why they can fail but only a single reason why the pass. Thus,
the preflight checks should cast the widest net possible.

The importance of preflight checks cannot be understated. Many
developers have not been introduced to this concept so it’s difficult
to grok what they’re doing. I’ve seen developers scratch their heads
and wonder "why do we even need these?"

I have two answers to that question.

First, I a real life example from my work at a previous company. A
team member was suspicious when I introduced a preflight checks for DB
access as I described earlier.  They were skeptical to the value and
didn’t see the point. Fast forward a few months into the future. The
team member made a change to the database configuration code. The PR
was peer reviewed and eventually deployed to production. The DB
connection preflight check failed because of the code changes, thus a
preventing production outage. The team member exclaimed "I love
preflight checks!" in the deploy slack channel.

Second, I offer the ideal of psychological safety. Gene Kim,
introduced the five ideals in his recent book The Unicorn Project.
Psychological safety is the fourth ideal. Put simply, developers need
the peace of mind that they may go about their work without fear of
negative consequences. Preflight checks ensure that known requirements
are met, thus increasing developer confidence that their changes will
work as expected. Ultimately, this improves flow and developer
happiness. What developer doesn’t want more confidence in their
changes working correctly in production?

I don’t know any such developer and I don’t think you do either. It’s
certainly not _you_ because you’re listening to this podcast!

So here’s the sequence of preflight checks in my deployment pipelines.
Time to put on my launch director hat.

This is the launch director preparing for production deploy.
Initiating preflight check sequence.

* Config? Config is go. Static configuration files passed static
  analysis.
* Credentials? Credentials are go for deploy. Validity confirmed.
* DNS? DNS is go for deploy. External services are resolvable.
* Traffic? Traffic is go for deploy. External services accepting
  incoming connections.
* Services? Go for deploy. End-to-end tests OK
* Dry run? Go for deploy. Dry-run completed successful with target
  configuration.

This is the LD on the deploy channel. Preflight checks are go for
deploy. Pipeline is cleared for release in T-minus 5 seconds.

Alright, let me step out of the control room and take the headset off.
Now I can elaborate on each check. The order uses the fail fast
approach.

The first config check is a sanity check. Many services use static
configuration files in JSON, YAML, or TOML. They’re usually parsed
when starting the application. So they should be parsed using a tool
like `jq`. This also includes the validity of any certificates.

The credentials check verifies credentials separate from external
services. Examples include AWS keys, instance profiles, and one-off
API keys or tokens. The check should call an "identity" operation. So,
if AWS access is required,  then running the `aws sts
get-caller-identity` command will validate access.

The DNS check uses the `dig` command. This verifies resolution of all
external services hostnames. Imagine looping over all environment
variables ending in `_URL` then calling `dig` with the hostname. This
is the first external services prerequisite.

The next traffic check uses the `netcat` command. This verifies that
configured hostnames accept traffic on the declared ports. Like the
DNS check, imagine looping over the variables, parsing the hostname
and port, then using the `netcat` command. If these two checks are go,
then the services check follows.

The services check runs the end-to-end tests I described early. Just
to reiterate, the goal is to verify the service can connect and use
the external service as required for normal operations.

I described the final dry-run check in a previous episode on the
config factor. Learn more at
[smallbatches.fm/6](https://smallbatches.fm/6). This check executes as
many code paths in the application as possible then stops just before
accepting incoming traffic. This verifies the application can load the
target configuration meaning nothing is missing, unparseable, or
unexpected.

This checklist hits the 80/20 sweet spot. It eliminates many
regressions and will certainly save you when you least expect it.
