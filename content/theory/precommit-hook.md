+++
author = "Adam Hawkins"
date = 2020-07-14T07:31:50Z
draft = false
summary = "The pre-commit prevents known bad commits from entering the deployment pipeline. Use it as tool to improve percent-complete-percent-accurate in your deployment pipeline."
tags = ["podcast", "continuous delivery"]
title = "Pre-Commit Hook"

+++

{{< transistor "https://share.transistor.fm/s/6abccef9" >}}

_This is an episode transcript. Visit the [podcast
website](https://share.transistor.fm/s/6abccef9) for the full episode,
show notes, and freebies._

The Pre-Commit hook is a powerful tool for increasing quality in the
continuous delivery pipeline. The commit is the first step in the
pipeline, so any work done at this stage has down stream
ramifications. The hook provides developers with immediate feedback by
blocking bad commits. So what constitutes a bad commit?

Consider the question from a lean manufacturing perspective. One
fundamental idea lean is assuring quality at the source. Imagine an
automobile assembly line.

One step produces lug nuts. The next step uses the lug nut to mount
the wheels on the car. If the lug nuts are the wrong size, then the
wheels cannot be mounted. The assembly line stops as a result. This is
an outage. The assembly line may only resume after the lug nuts are
produced correctly and given to the next step.

There's a metric for this scenario. It’s "percent complete; percent
accurate", also known as percent-C-A.  This metric measures quality in
the value stream. The lug nut in the example was complete but not
accurate because it was not useable as-is. Checking quality at the
source prevents these regressions which could even turn into full
blown outages.

So what does percent-complete-percent-accurate mean for commits? It
means proposed changes are usable as is by downstream consumers. There
are two downstream consumers of commits: the deployment pipeline and
other engineers.

Commits that knowingly fail in the deployment pipeline should be
rejected. Allowing these commit to proceed through the pipeline only
creates waste. We’ve all been there waiting behind the build that
takes too long then fails on some dumb mistake like a typo of a
malformed build configuration file. That build should have never have
started.  Running static analysis in the pre-commit hook easily
prevents these regressions.

Commits are also code reviewed. This requires that other people read
and understand the code. Inconsistent style is jarring to reviewers.
It increases the time and effort to complete code reviews. It also
creates rework for the original authors. You know, just a few minutes
here and there, fixing this and that, then waiting for builds, and
eventually getting an approval. Again, this is a waste. These
regressions are easily prevented by adding linting and formatting in
the pre-commit hook. Then it’s not possible to push commits containing
known rework conditions.

This is just static analysis and automated error correction. The key
is automation. If the process is not automated then it’s just not
happening.

After static analysis then run _some_ tests. I say some because it’s
likely impractical to run the entire suite in pre-commit hook. Instead
run the fastest tests or the most frequently failed tests, or just the
tests associated with files staged in the commit. The objective is
quickly fail known bad commits. In other words, fail fast.

Theses practices will increase the quality of individual commits and
provide developers fast feedback on correctness. Here’s an outline for
a pre-commit hook you can add to your projects:

1. Run static analysis on all files staged for a commit. Use tools
   like `eslint`, `shellcheck`, `rubocop`, `yaml-lint`, `jsonlint`,
   etc. Use the "autocorrect" option to automatically make stylistic
   changes.
2. Run static analysis on all configuration files staged for the
   commit. I’m referring to files like `circleci.yml` or `travis.yml`.
   These files are read by the pipeline itself, so errors here would
   definitely break the pipeline.  Validating them with the provided
   CLI prevents obvious regressions.
3. Auto-format code using tools like `prettier` or `go fmt` and be
   free from code formatting bike shedding.
4. Run those fast tests! Any file staged in the commit should be
   caught by some linter or static analysis tool. If not, then the
   pre-commit hook should fail. This requires developers to either
   update the linting configuration to handle the new file or
   explicitly ignore it. This ensures that files introduced to the
   codebase are covered by the pre-commit hook.

When downstream failures occur in the deployment pipeline, consider
preventing them by improving the pre-commit hook. Overtime the
percent-complete-percent accurate will increase. Feels good right?
