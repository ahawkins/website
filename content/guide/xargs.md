---
title: "xargs(1)"
author: "Adam Hawkins"
date: 2021-03-18T21:06:31-10:00
toc: true
tags:
  - shell
  - bash
---

> xargs - build and execute command lines from standard input

`xargs` translates arguments to commands. This effectively means you
can run one command per argument, or forward all arguments to one
command . Here's some examples to make it stick. We'll cover the finer
details later.

    # Stop all running Docker container ids
    $ docker ps -q | xargs docker stop
    # Get logs for all running docker containers
    $ docker ps -q | xargs -L1 docker logs

These two examples demonstrate the common uses. The first commands
take lists the all running Docker container ids and forwards them to
`docker stop`. Here's what this looks like in a verbose mode:

    $ docker ps -q | xargs -t docker stop
    docker stop 23489abc8ac 891bcadea134

The `-t` option instructs `xargs` to print the command before
executing it. `xargs` essentially looped over all arguments. Apply
`-t` to the second example to see the difference:

    $ docker ps -q | xargs -t -L1 docker logs
    docker logs 891bcadea134
    docker logs 23489abc8ac

The `-L` option controls the number of arguments applied to the given
command. `xargs -L1` executes one command per argument. `xargs`
without `-L` executes one command with all arguments. Naturally you
can control the number invocations by changing the `-L` option.

## Use Case

Use `xargs` when you need to run a single command against multiple
arguments. Do not use `xargs` if you need to execute logic against
each argument (such as if x, then y) or work with pipes. Use `while`
loop in that case. `xargs` is essentially your one-liner chainsaw! Use
without `-L` when the command supports multiple arguments (e.g the
command processes all arguments given). Use with `-L1` when the
command accepts a single argument.

## Signature & Key Options

    xargs [options] [command [initial-arguments]]

`xargs`'s signature is straight forward. It does not very based on
options. We already discussed `-L` to control executions and `-t` to
print the command before running it. These two options cover 80% of
use cases in my experience. Onto the other 20%.

`xargs` drops the arguments onto the end of `command` by default. So
what do you do if you need to apply options/arguments after the
argument? You use `-I`.`-I` provides the "replacement string". This is
effectively a template variable in the argument list.

Here's an example using the `service` command. `service` looks like
this: `service NAME ACTION`. `NAME` and `ACTION` are required. Here's
an example: `service http stop`. You could not use `xargs` directly
with `service`because `NAME` is not the last arguments. You can with
`-I`.

    # assume a list of names in services.txt
    $ cat services.txt | xargs -L1 -I {} service {} stop

Here `{}` is the replacement variable. `xargs` replaces all `{}`
occurrences in the arguments. `-I` has a hidden gotcha. The value
should not be a shell control character (which vary per shell; hint:
`fish`)! You could not use `#` because that's a comment character, nor
would you use `|` since that's for redirects. Use `{}` (by convention)
in sh/bash/zh or `%` in fish.

`-I` replaces the `-R` number of occurrences. `-R` defaults to. Read
manual on `-J` for an alternate replacement approach.

`xargs` supports parallel execution via `-P`. This is easier than
working with `parallel`. Combine with `$(nproc)` to execute the
correct number of commands for machine's processor.

## BSD vs GNU vs Busybox

`xargs` varies slightly (and annoyingly so) between BSD, GNU, and
Busybox. They share the same signature, but support different options.

- GNU `xargs` supports a `-r` / `--no-run-if-empty`. This is useful
  when argument list (perhaps generated dynamically) may be empty. GNU
  `xargs` exits successfully when this option and an empty argument
  list. BSD `xargs` does not support this option and fails if the
  argument list is empty.
- BSB `xargs` does not have `--verbose`. BSD uses `-t`, while GNU
  supports `-t` and `--verbose`.
- GNU `xargs` supports `-p` / `--interactive` to confirm individual
  commands before execution.
- BSD `xargs` does not support long options.
- Both versions run `command` against all arguments. Neither have an
  option to stop if `command` fails on one argument.
- Busybox `xargs` uses `-n` instead of `-L`

## Protips

- Use `-I @`. This is a single character that does not need escaping
  and works across all shells (Fish included). Don't believe the `{}`
  hype.
