---
title: "Bash Bootcamp: Hello World"
author: "Adam Hawkins"
date: 2021-06-04T22:39:56-10:00
tags:
  - shell
  - bash
description: |
  Beginner friendly "Hello World" with Bash
---

Every programming book starts off with the classic "Hello World"
program. The program simply prints the text "Hello World". This is
simple enough to do in bash.

```bash
#!/usr/bin/env bash

echo "Hello World"
```

How does this work? The first line is the "shebang". It indicates to
the shell how to execute this file. I use `/usr/bin/env bash` because
one can never never be certain where the bash executable lives on a
given system (maybe `/bin/bash`, or even `/usr/local/bin/bash`). I've
never had such a problem with `/usr/bin/env bash`. The following lines
are executable bash commands. The `echo` built in command prints text
to standard output. So save this file on your system as `hello-world`,
then `chmod +x hello-world`, and finally run `./hello-world`.
Naturally your computer will say hello to you.

Great, simple enough! Now let's parameterize this program so it can
say hello to a particular person. This quick exercise illustrates how
bash handles arguments. Bash programs (and functions) take any number
of arguments. Bash programs also do not explicitly declare their
arguments. Programs receive their arguments in numbered variables.
These are also referred to as "positional arguments". This is
demonstrated below.

```bash
#!/usr/bin/env bash

echo "Hello $1"
```

Invoke this program by running `./hello-world bob`. Naturally you'll
see a nice greeting on the screen. The `$1` variable refers to the
first argument given on the command line. You may ask what about `$0`?
That's a great question! `$0` holds the name of the program itself
(the first item in the command line argument list). See what's
happening? The arguments passed are available as numbered variables.
Running the program with `./hello-world bob dylan` assigns `dylan` to
`$2`. Now that we understand argument passing, we can update the
program to be strict about its arguments. After all the program can't
say hello if doesn't know who to greet. Luckily for us bash has built
in control structures. Let's update the program to check that it's
given an argument and act accordingly.

```bash
#!/usr/bin/env bash

name="$1"

if [[ -z "${name}" ]]; then
  echo "USAGE: $0 NAME" 1>&2
  exit 1
fi

echo "Hello ${name}"
```

There are few things going on here. First, the `name` variable is
assigned using `=`. Next we see the awkward looking bash `if` control
structure. `if` evaluates to true if the given command exits 0. The
`[[ ]]` is a built command for evaluating different conditions. In
this case the `-z ARG` tests the given value is zero length (blank).
Bash requires `then` keyword followed by the code to execute. The `fi`
ends the `if` control structure. Inside the if block the usage
instructions are printed to stderr via output redirection (`1>&2`).
Next `exit` sets the exit status and terminates the process. Naturally
we exit non zero because the command failed. This program is not big
by any means but it mirrors structure for larger programs: declare
named variables, check arguments/options, then perform the task.
Patterns appear in all programming programs, this enables similar
problems to be solved in the same way.

[style guide]: https://google.github.io/styleguide/shell.xml
[shellcheck]: https://www.shellcheck.net/
